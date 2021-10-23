---
layout: default
title: Voyajer
parent: aura
---
# Metadata Type
CustomObject

# Name
Voyajer
## Fields
### Voyajer

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### Voyajer

```
<aura:component
  implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction"
  access="global"
  controller="VoyajerController"
>
  <ltng:require styles="{!$Resource.RoadRebelUtils+'/css/all.css'}" />
  <ltng:require
    scripts="{!$Resource.RoadRebelUtils+'/js/jquery-3.3.1.min.js'}"
    afterScriptsLoaded="{!c.loadJquery}"
  />
  <aura:attribute
    type="VoyajerController.Client"
    name="client"
    default="{ userInfo: {}, preferencesAvailable: [], preferencesSelected: []}"
  />
  <aura:attribute
  type="Object[]"
  name="theSelectedBidOptions"
  default="[]"
/>       

  <aura:attribute
    type="Boolean"
    name="openSelectOptionsAlert"
    default="false"
  />
  <aura:attribute type="String" name="communityNotes" default="" />
  <aura:attribute type="String" name="modalTitle" default="" />
  <aura:attribute type="Boolean" name="showCommunityNote" default="false" />
  <aura:attribute type="List" name="productions" default="[]" />
  <aura:attribute type="List" name="theSelectedBids" default="[]" />
  <aura:attribute type="List" name="bidOptions" default="[]" />
  <aura:attribute type="List" name="compareList" default="[]" />
  <aura:attribute type="List" name="itineraries" default="[]" />
  <aura:attribute type="List" name="countries" default="[]" />
  <aura:attribute type="List" name="bidsSelected" />
  <aura:attribute
    type="List"
    name="lodgingPreferencesAvailable"
    default="[{ label: 'Airports', value: 'Airports' }]"
  />
  <aura:attribute
    type="User"
    name="userLogged"
    default="{'sobjectType' : 'User'}"
  />
  <aura:attribute type="List" name="lsDocuments" default="[]" />
  <aura:attribute type="List" name="lodgingRecords" default="[]" />
  <aura:attribute type="List" name="lsDocumentsAux" default="[]" />
  <aura:attribute type="String" name="sitePrefix" default="" />
  <aura:attribute type="String" name="userProfile" default="Forbidden" />
  <aura:attribute type="String" name="userName" />
  <aura:attribute type="String" name="officePreference" default="RRU" />
  <aura:attribute type="String" name="productionOfficePreference" default="" />
  <aura:attribute type="String" name="hco" default="" />
  <aura:attribute type="String" name="productionName" />
  <aura:attribute type="String" name="productionCompany" />
  <aura:attribute type="String" name="mainContent" />
  <aura:attribute type="String" name="menuSelected" />
  <aura:attribute type="String" name="productionSelected" default="" />
  <aura:attribute type="String" name="optionRecordId" />
  <aura:attribute type="String" name="typeOfService" />
  <aura:attribute type="Object" name="itineraryData" />
  <aura:attribute type="Object" name="recordTypes" />
  <aura:attribute type="Object" name="serviceData" />
  <aura:attribute type="Object" name="optionDetailRecord" />
  <aura:attribute type="Object" name="closeOutData" />
  <aura:attribute type="Object" name="vendorData" />
  <aura:attribute type="Object" name="bidData" />
  <aura:attribute type="Integer" name="optionDetailRecordId" />
  <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
  <aura:attribute type="Integer" name="bidOptionsSize" />
  <aura:attribute type="String" name="serviceId" />
  <aura:attribute type="String" name="serviceType" />
  <aura:attribute type="String" name="serviceDateInAndOut" />
  <aura:attribute type="String" name="serviceCityName" />
  <aura:attribute type="String" name="productionAssocUserName" />
  <aura:attribute type="String" name="productionAssocUserPhone" />
  <aura:attribute type="String" name="productionAssocUserEmail" />
  <aura:attribute type="String" name="productionAssocRole" />
  <aura:attribute type="String" name="bidRecordId" />
  <aura:attribute type="Object" name="reservationDetail" />
  <aura:attribute type="List" name="bids" default="[]" />
  <aura:attribute type="String" name="bidName" />
  <aura:attribute type="Object" name="contactUsData" />
  <aura:attribute type="Object" name="revenueVatData" />
  <aura:attribute type="List" name="bidOptionsFiltered" default="[]" />
  <aura:attribute name="startDate" type="String" />
  <aura:attribute name="endDate" type="String" />
  <aura:attribute name="selectedLookupId" type="String" />
  <aura:attribute name="selectedPillText" type="String" />
  <aura:handler
    name="change"
    value="{!v.theSelectedBids}"
    action="{!c.handleChangeSelectedBids}"
  />

  <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
  <aura:handler
    name="callToParent"
    action="{!c.handleCommunicationEvent}"
    event="c:VoyajerCallToParent"
  />
  <aura:handler
    name="callToParentGetRevenue"
    action="{!c.handleCommunicationEventGetRevenue}"
    event="c:VoyajerCallToParentGetRevenue"
  />
  <aura:handler
    name="callToParentUpdateVAT"
    action="{!c.handleCommunicationEventUpdateVAT}"
    event="c:VoyajerCallToParentUpdateVAT"
  />
  <aura:registerEvent type="c:VoyajerCallToChild" name="callToChild" />
  <div class="box">
    <lightning:spinner
      aura:id="loadingPage"
      alternativeText="Loading"
      size="large"
    />
    <div class="topNavigator">
      <div class="logoNavigator">
        <img src="{!$Resource.CommunityImages+'/LogoRR.png'}" />
      </div>
      <div class="buttonsNavigator">
        <div
          class="centerDiv"
          onclick="{!c.loadDashboardContent}"
          style="
             {
              !v.maincontent=='dashboard'?'border-bottom: 0.25em solid #0065ff;': '';
            }
          "
        >
          <div class="hideOnMobile">Dashboard</div>
          <div class="showOnMobile">
            <lightning:icon
              iconName="utility:screen"
              alternativeText="Dash."
              size="small"
            />
          </div>
        </div>
        <!--<div class="centerDiv" onclick="{!c.loadReportsContent}" style="{!v.mainContent=='reports'? 'border-bottom: 0.25em solid #0065ff;':''}">-->
        <!--<div class="hideOnMobile">Reports</div>-->
        <!--<div class="showOnMobile"><lightning:icon iconName="utility:copy_to_clipboard" alternativeText="Rep." size="small" /></div>-->
        <!--</div>-->
        <!--<div class="centerDiv" onclick="{!c.loadContactUsContent}" style="{!v.productionSelected != '' ? (v.mainContent=='contactus'? 'border-bottom: 0.25em solid #0065ff;':'') : 'display:none;'}">
                    <div class="hideOnMobile">Contact Us</div>
                    <div class="showOnMobile"><lightning:icon iconName="utility:groups" alternativeText="Rep." size="small" /></div>
                </div>-->

        <aura:if isTrue="{!not(empty(v.contactUsData))}">
          <div
            class="centerDiv"
            onclick="{!c.loadContactUsContent}"
            style="{!v.productionSelected != '' ? (v.mainContent=='contactus'? 'border-bottom: 0.25em solid #0065ff;':'') : 'display:none;'}"
          >
            <div class="hideOnMobile">Contact Us</div>
            <div class="showOnMobile">
              <lightning:icon
                iconName="utility:groups"
                alternativeText="Rep."
                size="small"
              />
            </div>
          </div>
        </aura:if>
      </div>
      <div class="profileNavigator">
        <aura:if isTrue="{!v.client.userInfo.User_Profile__c!='Forbidden'}">
          <div class="greeting hideOnMobile">
            <span style="padding-right: 0.3em">Hello,</span>
            <aura:if isTrue="{!v.client.userInfo.User_Profile__c=='Customer'}">
              <a href="javascript:void(0);" onclick="{!c.loadUserContent}"
                >{!v.client.userInfo.Name}</a
              >
              <aura:set attribute="else">
                <a href="javascript:void(0);" onclick="{!c.loadUserContent}"
                  >{!v.client.userInfo.Contact.Account.Name}</a
                >
              </aura:set>
            </aura:if>
          </div>
          <div
            class="centerDiv"
            onclick="{!c.loadUserContent}"
            style="{!v.mainContent=='user' || v.mainContent=='vendor'? 'border-bottom: 0.25em solid #0065ff;':''}"
          >
            <lightning:avatar
              src="{!v.client.userInfo.SmallPhotoUrl}"
              variant="circle"
              initials="{!v.client.userInfo.Initials__c}"
              alternativeText="{!v.client.Name}"
            />
          </div>
          <div
            class="centerDiv"
            onclick="{!c.logout}"
            style="
               {
                !v.maincontent=='logout'?'border-bottom: 0.25em solid #0065ff;': '';
              }
            "
          >
            <lightning:avatar
              src=""
              fallbackIconName="utility:logout"
              variant="square"
              alternativeText="Log Out"
              class="logoutIcon"
            />
          </div>
        </aura:if>
      </div>
    </div>
    <div class="mainPageContainer">
      <aura:if isTrue="{!v.mainContent=='dashboard'}">
        <c:VoyajerDashboard
          userLogged="{!v.client.userInfo}"
          productions="{!v.productions}"
          mainContent="{!v.mainContent}"
          officePreference="{!v.officePreference}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          openSelectOptionsAlert="{!v.openSelectOptionsAlert}"
          communityNote="{!v.communityNote}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='actions'}">
        <c:VoyajerActions
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          itineraries="{!v.itineraries}"
          optionRecordId="{!v.optionRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='itinerary'}">
        <c:VoyajerItinerary
          mainContent="{!v.mainContent}"
          menuSelected="{!v.menuSelected}"
          productionSelected="{!v.productionSelected}"
          itineraryData="{!v.itineraryData}"
          recordTypes="{!v.recordTypes}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousing'}">
        <c:VoyajerOptionsHousing
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          userProfile="{!v.userProfile}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptions}"
          bidOptionsFiltered="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
          bidsSelected="{!v.bidsSelected}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}"                       
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"                  
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsSubmitMultiple'}">
        <c:VoyajerOptionsEventsSubmit
          mainContent="{!v.mainContent}"
          housingId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          officePreference="{!v.officePreference}"
          bidOptions="{!v.bidOptionsFiltered}"
          bidOptionsSize="{!v.bidOptionsSize}"
          itineraryData="{!v.itineraryData}"
          lodgingRecords="{!v.lodgingRecords}"
          bidsSelected="{!v.bidsSelected}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingDetail'}">
        <c:VoyajerOptionsHousingDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
          preferencesSelected="{!v.client.preferencesSelected}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingReviewSubmit'}">
        <c:VoyajerOptionsHousingReviewSubmit
          mainContent="{!v.mainContent}"
          housingId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          officePreference="{!v.officePreference}"
          bidOptions="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingCompare'}">
        <c:VoyajerOptionsHousingCompare
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptions}"
          compareList="{!v.compareList}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGT'}">
        <c:VoyajerOptionsGT
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTDetail'}">
        <c:VoyajerOptionsGTDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTCompare'}">
        <c:VoyajerOptionsGTCompare
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          compareList="{!v.compareList}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTReviewSubmit'}">
        <c:VoyajerOptionsGTReviewSubmit
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsFreight'}">
        <c:VoyajerOptionsFreight
          mainContent="{!v.mainContent}"
          itinerarySelected="{!v.optionRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAir'}">
        <c:VoyajerOptionsAir
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAirDetail'}">
        <c:VoyajerOptionsAirDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAirReviewSubmit'}">
        <c:VoyajerOptionsAirReviewSubmit
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='overview'}">
        <c:VoyajerItineraryOverview
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          optionRecordId="{!v.optionRecordId}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}"                           
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"                           
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='documents'}">
        <c:VoyajerDocuments
          mainContent="{!v.mainContent}"
          userProfile="{!v.client.userInfo.User_Profile__c}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          productionName="{!v.productionName}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          lsDocuments="{!v.lsDocuments}"
          lsDocuments_org="{!v.lsDocumentsAux}"
          bidName="{!v.bidName}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}" 
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"  
        ></c:VoyajerDocuments>
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='newProduction'}">
        <c:VoyajerNewProduction
          userLogged="{!v.client.userInfo}"
          mainContent="{!v.mainContent}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='reports'}">
        <c:VoyajerReports userLogged="{!v.client.userInfo}" />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='contactus'}">
        <c:VoyajerContactUs contactUsData="{!v.contactUsData}" />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='user'}">
        <c:VoyajerUser
          userLogged="{!v.client.userInfo}"
          lodgingPreferencesAvailable="{!v.client.preferencesAvailable}"
          lodgingPreferencesSelected="{!v.client.preferencesSelected}"
          countries="{!v.countries}"
          countryAndStates="{!v.client.countryAndStates}"
        />
      </aura:if>

      <aura:if isTrue="{!v.mainContent=='closeOutHousing'}">
        <c:VoyajerCloseOutHousing
          mainContent="{!v.mainContent}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
          productionSelected="{!v.productionSelected}"
          officePreference="{!v.officePreference}"
          closeOutData="{!v.closeOutData}"
          closeOutRevenue = "{!v.revenueVatData}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='dashboardBids'}">
        <c:VoyajerDashboardBids
          userProfile="{!v.client.userInfo.User_Profile__c}"
          userLogged="{!v.client.userInfo}"
          bids="{!v.bids}"
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          bidRecordId="{!v.bidRecordId}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendor'}">
        <c:VoyajerVendor
          userLogged="{!v.client.userInfo}"
          userProfile="{!v.userProfile}"
          vendorData="{!v.vendorData}"
          countries="{!v.countries}"
          countryAndStates="{!v.client.countryAndStates}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorActions'}">
        <c:VoyajerVendorActions
          mainContent="{!v.mainContent}"
          bidRecordId="{!v.bidRecordId}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
          itineraries="{!v.itineraries}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorReservationHousingDetails'}">
        <c:VoyajerVendorReservationHousing
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          optionRecordId="{!v.optionRecordId}"
          bidRecordId="{!v.bidRecordId}"
          reservationDetail="{!v.reservationDetail}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorReservationGTDetails'}">
        <c:VoyajerVendorReservationGT
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          bidRecordId="{!v.bidRecordId}"
          reservationDetail="{!v.reservationDetail}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='bidVendorHousing'}">
        <c:VoyajerVendorHousingBid
          mainContent="{!v.mainContent}"
          userProfile="{!v.userProfile}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionOfficePreference="{!v.officePreference}"
          bidData="{!v.bidData}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='bidVendorGround'}">
        <c:VoyajerVendorGroundBid
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionOfficePreference="{!v.officePreference}"
          bidData="{!v.bidData}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
        />
      </aura:if>
    </div>
  </div>
</aura:component>
```
### Voyajer

```
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600&display=swap');

.THIS {
    display: flex;
    height: 100%;
    font-family: 'Poppins', sans-serif;
    flex-direction: column;
}

.THIS .showOnMobile,
.THIS .showOnTablet {
    display: none;
}

.THIS .hideOnTablet {
    display: inline-flex;
}

.THIS .hideOnMobile {
    display: block;
}

.THIS h1 {
    font-size: 1.5rem;
}

.THIS .titleIcon {
    padding-right: 0.5em;
    color: #606060;
}

.THIS .topNavigator {
    height: 4.375em;
    background-color: white;
    border-bottom: 1px solid #9f9f9f;
    display: flex;
    font-size: 0.75rem;
}

.THIS .logoNavigator {
    display: flex;
    height: 100%;
}

.THIS .logoNavigator > img {
    max-height: 100%;
    max-width: 100%;
}

.THIS .buttonsNavigator {
    align-items: center;
    display: flex;
    flex: 1;
    font-size: .75rem;
    font-weight: 500;
}

.THIS .profileNavigator,
.THIS .profileNavigator > div {
    padding: 0 0.5em;
    display: flex;
    align-items: center;
    justify-content: center;
}

.THIS .profileNavigator > div {
    height: 100%;
}

.THIS .centerDiv {
    align-items: center;
    justify-content: center;
    display: flex;
    height: 100%;
    margin-left: 1.5em;
    padding: 0 1em;
    border-bottom: 0.25em solid transparent;
    cursor: pointer;
}

.THIS .centerDiv:last-child {
    margin-right: 1.5em;
}

.THIS .centerDiv:hover {
    border-bottom: 0.25em solid #00b4ff;
}

.THIS .centerDiv > div {
    margin-top: 0.25em;
}

.THIS .logoutIcon .slds-icon {
    fill: #0065ff;
}

.THIS .profileNavigator .greeting {
    margin-right: -0.5em;
}

.THIS .profileNavigator .greeting > a {
    white-space: nowrap;
    max-width: 8em;
    overflow: hidden;
    text-overflow: ellipsis;
}

.THIS .mainPageContainer {
    background-color: #f0f0f0;
    display: flex;
    flex: 1;
    overflow-y: auto;
}

.THIS .mainPageContainer > div {
    display: flex;
    flex: 1;
    overflow-y: auto;
}

.THIS .mainMenu {
    background: #282828;
    color: white !important;
    float: left;
    height: 100%;
    overflow-y: auto;
    width: 15em;
    font-size: 0.75rem;
}

.THIS .sideBarProfile .slds-nav-vertical__item:hover::before {
    background: rgba(21, 137, 238, 0.25);
}

.THIS .sideBarProfile .slds-nav-vertical__action,
.THIS .sideBarItinerary .slds-nav-vertical__action {
    color: white !important;
    padding: 0.5em 1.25em;
}

.THIS .sideBarProfile .slds-nav-vertical__action:hover {
    box-shadow: #00b4ff 0.125rem 0px 0px inset;
}

.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarItinerary .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action:hover,
.THIS .sideBarItinerary .slds-is-active .slds-nav-vertical__action:hover {
    box-shadow: #00b4ff 0.25rem 0px 0px inset;
}

.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action:hover {
    background: #0065ff;
}

.THIS .sideBarItinerary .slds-nav-vertical__item:hover::before {
    background: transparent;
}

.THIS .sideBarItinerary .slds-nav-vertical__action:hover {
    box-shadow: none;
}

.THIS .sideBarItinerary .slds-nav-vertical__action {
    cursor: default;
}

.THIS .sideBarItinerary .slds-nav-vertical__item.slds-is-active:hover:before {
    background: rgba(21, 137, 238, 0.1) !important;
}

.THIS .sideBarItinerary .slds-nav-vertical__action svg,
.THIS .sideBarProfile .slds-nav-vertical__action svg {
    fill: white !important;
}

.THIS .sideBarItineraryIcon {
    width: 1.5rem;
}

.THIS .checkpoint {
    position: absolute;
    right: 0;
    margin-right: 1em;
    color: #00b4ff;
    font-size: 1rem;
}

.THIS .checkpointIcon {
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.THIS .checkpointBackground {
    width: 0.65em;
    height: 0.65em;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
}

.THIS .pageContent {
    display: flex;
    flex: 1;
    flex-direction: column;
    overflow-y: auto;
    font-size: 0.875rem;
}

.THIS .pageContentSpaces {
    padding: 2em;
    max-width: 82em;
    width: 100%;
    margin: 0 auto;
}

.THIS .page-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5em;
}

.THIS .pageContent h1,
.THIS .pageContent h2 {
    flex: 1;
    font-size: 1.45rem;
    font-weight: 600;
}

.THIS .pageContent h1 {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.THIS .pageContent h2 {
    font-weight: 500;
}

.THIS .pageContent h3 {
    font-size: 1.25rem;
}

.THIS .page-section {
    display: flex;
    flex-direction: column;
}

.THIS .page-section-buttons {
    display: flex;
    justify-content: space-between;
    width: 100%;
    align-items: flex-end;;
}

.THIS .page-section-buttons > div {
    display: flex;
    margin-top: 0.5em;
}

.THIS .page-section-content_header {
    display: flex;
    text-align: center;
    padding: 2em 2em 0;
    flex-direction: column;
}

.THIS .page-section-content_center {
    text-align: center;
    display: flex;
    justify-content: center;
    flex-flow: wrap;
}

.THIS .page-section-services_center {
    text-align: center;
    display: flex;
    justify-content: space-evenly;
    flex-flow: wrap;
    max-width: 50em;
    width: 100%;
    margin: 1.5em 0;
}

.THIS .pageContentForm,
.THIS .pageContentDashboard {
    background-color: white;
    text-align: justify;
    padding: 2em;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
}

.THIS .pageContentForm p {
    line-height: 2;
    margin-bottom: 1em;
}

.THIS .pageContentForm p:last-child {
    margin-bottom: 0;
}

.THIS .pageContentDashboard {
    padding: 1em;
    font-size: 0.8rem;
}

.THIS .pageContentDashboardVendor {
    padding: 2em;
    font-size: 0.8rem;
}

.THIS .dashboardPill {
    width: 100%;
    color: #e00000;
}

.THIS .dashboardPill svg {
    fill: #e00000;
}

.THIS .dashboardPill .slds-pill__action {
    border: none;
}

.THIS .formColumnTwoChilds,
.THIS .formColumnThreeChilds,
.THIS .formColumnTwoChildsWithDate,
.THIS .formColumnThreeChildsDependant,
.THIS .formColumnFourChildsDependant {
    display: flex;
    width: 100%;
    min-width: 0;
}

.THIS .formColumnTwoChilds > *,
.THIS .formColumnThreeChilds > *,
.THIS .formColumnTwoChildsWithDate > * {
    width: 100%;
}

.THIS .formColumnTwoChildsWithDate > *:last-child {
    width: 60%;
}

.THIS .formColumnThreeChildsDependant > *:first-child,
.THIS .formColumnFourChildsDependant > *:first-child {
    width: auto;
    flex: 1;
}

.THIS .formColumnThreeChildsDependant > *:last-child {
    display: flex;
    flex: 2;
    flex-direction: column;
    margin-left: -1.5em;
}

.THIS .formColumnFourChildsDependant > *:last-child {
    display: flex;
    flex: 3;
    flex-direction: column;
    margin-left: -1.5em;
}

.THIS .formField {
    min-width: 0;
    width: 100%;
    padding: 0px 0.25rem;
    margin-bottom: 0.5rem;
}

.THIS .formFieldHorizontal {
    display: flex;
}

.THIS .formFieldHorizontal > .slds-form-element {
    flex: 1;
}

.THIS .formField label {
    overflow-wrap: break-word;
    display: inline-block;
    color: rgb(105, 105, 105);
    font-size: 1em;
    font-weight: 500;
    padding-right: 0.5rem;
    padding-top: 0.25rem;
    margin-bottom: 0.25rem;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.THIS .formField > label > span {
    font-size: 0.8em;
    font-weight: 400;
    padding-left: 0.75em;
}

.THIS .formColumnBlank {
    display: flex;
    width: 100%;
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

.THIS .slds-button {
    border-radius: 3em;
    text-transform: uppercase;
}

.THIS .formButtonBrand {
    background-color: #0065ff;
}

.THIS .formButtonBrand:hover,
.THIS .formButtonBrand:focus {
    background-color: #0051ce;
}

.THIS .formButtonBrandLight {
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .formButtonBrandLight:hover,
.THIS .formButtonBrandLight:focus {
    background-color: #009cf1;
    border-color: #00a4fb;
}

.THIS .formButtonBrandInverse {
    color: #0065ff;
    border-color: #0065ff;
}

.THIS .formButtonBrandInverse:hover,
.THIS .formButtonBrandInverse:focus {
    background-color: #dfebff;
}

.THIS .formButtonBrandInverse:focus {
    box-shadow: 0px 0px 2px 2px #afceff;
}

.THIS .formButtonDestructive {
    background-color: #e00000;
    color: white;
}

.THIS .formButtonDestructive:hover,
.THIS .formButtonDestructive:focus {
    background-color: #bf0000;
}

.THIS .formButtonDestructive:focus {
    box-shadow: 0px 0px 2px 2px #ff9b9b;
}

.THIS .formButtonDestructiveInverse {
    color: #e00000;
    border-color: #e00000;
}

.THIS .formButtonDestructiveInverse:hover,
.THIS .formButtonDestructiveInverse:focus {
    background-color: #ffeaea;
}

.THIS .formButtonDestructiveInverse:focus {
    box-shadow: 0px 0px 2px 2px #ff9b9b;
}

.THIS .formButtonSuccess {
    background-color: #17b216;
    color: white;
}

.THIS .formButtonSuccess:hover,
.THIS .formButtonSuccess:focus {
    background-color: #019a00;
}

.THIS .formButtonSuccess:focus {
    box-shadow: 0px 0px 2px 2px #17b216;
}

.THIS .formButtonAction {
    background-color: #ec4518;
    color: white;
    border-color: #ff3600;
}

.THIS .formButtonAction:hover,
.THIS .formButtonAction:focus {
    background-color: #e83100;
}

.THIS .formButtonAction:focus {
    box-shadow: 0px 0px 2px 2px #bf2900;
}

.THIS .clear {
    color: #e00000;
}

.THIS .page-section_record {
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    width: 100%;
    border: 1px solid #dbdbdb;
    margin: 0.5em 0 1em;
}

.THIS .page-section_record > div,
.THIS .page-section_record > div > div,
.THIS .recordDetails > div {
    display: flex;
}

.THIS .recordBodySideColumn {
    min-width: 3.25em;
    border-right: 1px solid #dbdbdb;
    justify-content: center;
    background-color: #f7f9fe;
    color: #9f9f9f;
    font-weight: 500;
    align-items: center;
}

.THIS .recordBodySideColumn span {
    font-size: 1.25em;
}

.THIS .recordHeader {
    height: 3.25em;
}

.THIS .recordTitle {
    padding: 0 1.5em;
}

.THIS .recordTitle,
.THIS .recordTitleText {
    align-items: center;
    flex: 1;
    overflow: hidden;
}

.THIS .recordTitle > div {
    align-items: center;
    display: flex;
    height: 100%;
}

.THIS .recordTitleText > div {
    font-weight: 500;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

.THIS .recordTitleText .location {
    color: #00b4ff;
    font-weight: 600;
}

.THIS .recordTitleText .dates {
    color: #606060;
    min-width: 10rem;
    text-align: left;
    padding-left: 0.5em;
    border-left: 2px solid #9f9f9f;
    margin-left: 0.5em;
}

.THIS .recordTitleButton {
    padding-left: 0.5em;
}

.THIS .recordBody {
    border-top: 1px solid #dbdbdb;
}

.THIS .recordBodyContent {
    display: flex;
    flex: 1;
    flex-direction: column;
    width: 100%;
    padding: 1.5em;
    min-width: 0;
}

.THIS .recordDetails {
    border: 1px solid #dbdbdb;
    margin-top: 1.5em;
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    width: 100%;
}

.THIS .recordDetails .recordTitle {
    background-color: #f0f0f0;
    height: 3.75em;
}

.THIS .recordDetails .recordBodyContent {
    border-top: 1px solid #dbdbdb;
}

.THIS .recordActions {
    margin-top: 1.5em;
}

.THIS .titleArrow {
    fill: white !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    display: block;
}

.THIS .tableRow > div > span {
    white-space: pre-wrap; /*update*/
}

.THIS .tableLocation {
    flex: 2;
}

.THIS .tableTripRow {
    display: flex;
    width: 100%;
    flex: 1;
    min-width: 0;
}

.THIS .tableTripRow > div {
    width: 100%;
}

.THIS .tripInfo {
    flex: 2;
}

.THIS .tabIcon {
    color: #606060;
    font-size: 1.25rem;
}

.THIS .buttonColumn {
    display: flex !important;
    width: 2em;
    padding: .25em 0 !important;
    align-items: flex-start;
    justify-content: flex-start;
}

@media (max-width: 1200px) {
    .THIS .showOnTablet {
        display: inline-flex !important;
    }
    
    .THIS .hideOnTablet {
        display: none !important;
    }
}

@media (max-width: 1024px) {
    .THIS .topNavigator {
        height: 3.5em;
    }
}

@media (max-width: 800px) {
    .THIS .pageContentSpaces {
        padding: 1.5em;
    }
    
    .THIS .pageContentForm {
        padding: 1em;
    }
    
    .THIS .page-section-buttons {
        flex-direction: column;
        width: 100%;
    }
    
    .THIS .page-section-buttons > div {
        width: 100%;
    }
}

@media (max-width: 550px) {
    .THIS .showOnMobile {
        display: block !important;
    }
    
    .THIS .hideOnMobile {
        display: none !important;
    }
    
    .THIS .mainMenu {
        width: 3.5em;
    }
    
    .THIS .pageContentSpaces {
        padding: 1em;
    }
    
    .THIS .formColumnThreeChildsDependant > *,
    .THIS .formColumnFourChildsDependant > * {
        width: 100%;
    }
    
    .THIS .page-section-buttons,
    .THIS .formColumnTwoChilds,
    .THIS .formColumnThreeChilds,
    .THIS .formColumnTwoChildsWithDate,
    .THIS .formColumnThreeChildsDependant,
    .THIS .formColumnFourChildsDependant {
        flex-wrap: wrap;
    }
    
    .THIS .formColumnThreeChildsDependant > *:last-child,
    .THIS .formColumnFourChildsDependant > *:last-child {
        flex-wrap: wrap;
        display: flex;
        flex-direction: column;
        margin-left: 0;
    }
    
    .THIS .page-section-buttons > div {
        justify-content: space-between;
    }
    
    .THIS .formColumnBlank {
        display: none;
    }
    
    .THIS .checkpoint {
        font-size: .75rem;
        top: 30%;
        right: 0;
    }
}

@media print {
    .THIS .mainPageContainer{
      overflow-y: unset !important;
    }
}
```
### VoyajerHelper

```
({
  checkCommunityNote: function (cmp) {
    var action = cmp.get("c.getCommunityNote");
    action.setParams({
      contactId: cmp.get("v.client").userInfo.ContactId,
      officePreference: cmp.get("v.officePreference")
    });
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var response = response.getReturnValue();
      })
    );
    $A.enqueueAction(action);
  },
  crud: function (component, methodName, data) {
    function alphanumeric(text) {
      if (typeof text !== "string") return false;
      if (!!text && text.length != 18) return false;
      for (var i = 0; i < text.length; i++) {
        var code = text.charCodeAt(i);
        if (
          !(code > 47 && code < 58) &&
          !(code > 64 && code < 91) &&
          !(code > 96 && code < 123)
        )
          return false;
      }
      return true;
    }
    var self = this;
    var action = component.get("c." + methodName);
    $A.util.removeClass(component.find("loadingPage"), "slds-hide");
    switch (methodName) {
      case "saveLodgingPreferences":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          preferences: component.get("v.client").preferencesSelected.join(";")
        });
        break;
      case "getProductions":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          officePreference: component.get("v.officePreference")
        });
        break;
      case "getCommunityNote":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          officePreference: component.get("v.officePreference")
        });
        break;
      case "getVendorProfile":
      case "getPropertyProfile":
      case "getPropertyInRoom":
      case "getPropertyOnSite":
      case "getFleetCoach":
      case "getFleetChauffeured":
      case "getFleetRental":
      case "getVendorPayment":
        action.setParams({
          accountId: component.get("v.client").userInfo.Contact.AccountId
        });
        break;
      case "getProductionItineraries":
      case "getMultipleOptions":
        action.setParams({
          productionId: component.get("v.productionSelected"),
          productionOfficePreference: component.get(
            "v.productionOfficePreference"
          )
        });
      case "getProductionServices":
      case "subimtProductionItineraries":
        action.setParams({
          productionId: component.get("v.productionSelected")
        });
        break;
      case "getLodgingPage":
      case "getGroundPage":
      case "getAirPage":
      case "getFreightPage":
        action.setParams({
          productionId: component.get("v.productionSelected"),
          productionOfficePreference: component.get(
            "v.productionOfficePreference"
          )
        });
        break;
      case "getVendorProductionBids":
        action.setParams({ bidId: component.get("v.bidRecordId") });
        break;
      case "createProduction":
      case "saveProductionServices":
      case "upsertItineraryRecord":
      case "deleteItineraryRecord":
      case "getCloseOutHousing":
      case "upsertCloseOutHousing":
      case "submitBidSelected":
      case "updateVendorProfile":
      case "upsertVendorContact":
      case "updatePropertyProfile":
      case "updatePropertyInRoom":
      case "updatePropertyOnSite":
      case "upsertVendorVehicle":
      case "updateFleetCoach":
      case "updateFleetChauffeured":
      case "updateFleetRental":
      case "updateVendorPayment":
      case "updateVendorHousingBid":
      case "updateVendorGroundBid":
      case "unabledVendorBid":
        action.setParams({ data: JSON.stringify(data) });
        break;
      case "getOptionsHousing":
        action.setParams({ housingId: component.get("v.optionRecordId") });
        break;
      case "getOptionsHousingDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getOptionsGT":
        action.setParams({ groundId: component.get("v.optionRecordId") });
        break;
      case "getOptionsGTDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getOptionsAir":
        action.setParams({ airId: component.get("v.optionRecordId") });
        break;
      case "getOptionsAirDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getVendorBids":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "getReservationHousingDetail":
        action.setParams({ bidRecordId: data.detailRecordId });
        break;
      case "getReservationGTDetail":
        action.setParams({ bidRecordId: data.detailRecordId });
        break;
      case "getContactUsData":
        action.setParams({
          productionId: component.get("v.productionSelected")
        });
        break;
      case "getDocuments":
        action.setParams({ serviceId: data.serviceId });
        break;
      case "saveDocument":
        action.setParams({
          fileName: data.docName,
          fileContentBase64: data.docContentBase64,
          fileReName: data.docReName,
          fileType: data.docType,
          entityId: data.docServiceId
        });
        break;
      case "getVendorContacts":
        action.setParams({
          accountId: component.get("v.client").userInfo.Contact.AccountId,
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "deleteVendorContact":
      case "deleteVendorVehicle":
        action.setParams({
          accountId: data.accountId,
          recordId: data.recordId
        });
        break;
      case "verifyOptionAccess":
        action.setParams({
          typeOfService: component.get("v.typeOfService"),
          optionRecordId: component.get("v.optionRecordId"),
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "verifyVendorAccess":
        action.setParams({
          typeOfService: component.get("v.typeOfService"),
          optionRecordId: component.get("v.optionRecordId"),
          accountId: component.get("v.client").userInfo.Contact.AccountId
        });
        break;
      case "getVendorHousingBid":
      case "getVendorGroundBid":
        action.setParams({
          recordId: component.get("v.optionRecordId"),
          accountId: component.get("v.client").userInfo.Contact.AccountId,
          isRRE: component.get("v.officePreference") == "RRE" ? true : false
        });
        break;
      case "updateVATData":
        action.setParams({data: JSON.stringify(data)});
      case "saveMultipleOptionsSelected":
        let theBidOptions = [];
        theBidOptions = component.get('v.theSelectedBidOptions');
        action.setParams({bidData : theBidOptions});
        console.log('bidOptions length :: ' + theBidOptions.length);
        break;
      default:
        break;
    }
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var state = response.getState();
        if (state === "SUCCESS") {
          var returnValue = response.getReturnValue();
          let noteFixed = "";   
          switch (methodName) {
            case "saveMultipleOptionsSelected":
              self.showMessage("success","Done!","Your options have all been updated.");
              self.crud(component, "getOptionsHousing", {});
              component.set("v.mainContent","dashboard");
              break;
            case "getClient":
              component.set("v.client", returnValue);
              //this.checkCommunityNote(component);
              var countries = [];
              for (var country in returnValue.countryAndStates.pickListMap)
                countries.push(country);
              component.set("v.countries", countries);
              component.set("v.recordTypes", returnValue.recordTypes);
              console.log(returnValue.userInfo.User_Profile__c);
              if (returnValue.userInfo.hasOwnProperty("Housing_Preference__c"))
                component.set(
                  "v.officePreference",
                  returnValue.userInfo.Housing_Preference__c
                );
              if (
                returnValue.userInfo.hasOwnProperty("User_Profile__c") &&
                returnValue.userInfo.User_Profile__c != "Forbidden"
              ) {
                component.set(
                  "v.userProfile",
                  returnValue.userInfo.User_Profile__c
                );
                if (returnValue.userInfo.User_Profile__c == "Customer") {
                  if (!!component.get("v.optionRecordId"))
                    self.crud(component, "verifyOptionAccess", {});
                  component.set("v.mainContent", "dashboard");
                } else {
                  if (!!component.get("v.optionRecordId")) {
                    component.set("v.mainContent", "dashboardBids");
                    if (
                      (alphanumeric(component.get("v.optionRecordId")) &&
                        (component.get("v.userProfile") == "HousingVendor" ||
                          component.get("v.userProfile") ==
                            "CorporateVendor") &&
                        component.get("v.typeOfService") == "optionsHousing") ||
                      (component.get("v.userProfile") == "GroundVendor" &&
                        component.get("v.typeOfService") == "optionsGT")
                    )
                      self.crud(component, "verifyVendorAccess", {});
                    else
                      self.showMessage(
                        "error",
                        "",
                        "You have no access to this record. Please contact Road Rebel team for support."
                      );
                  } else if (!!component.get("v.hco")) {
                    if (!alphanumeric(component.get("v.hco")))
                      self.showMessage(
                        "error",
                        "",
                        "You have no access to this record. Please contact Road Rebel team for support."
                      );
                    else {
                      component.set("v.serviceId", component.get("v.hco"));
                      component.set("v.mainContent", "closeOutHousing");
                    }
                  } else component.set("v.mainContent", "dashboardBids");
                }
              } else
                self.showMessage(
                  "error",
                  "Your are not a community user!",
                  "Your have no access to this page."
                );
              self.crud(component, "getCommunityNote", {});
              break;
            case "verifyOptionAccess":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              ) {
                component.set("v.productionSelected", returnValue.productionId);
                component.set("v.productionName", returnValue.productionName);
                self.crud(component, "getContactUsData", {});
                component.set(
                  "v.mainContent",
                  component.get("v.typeOfService")
                );
              } else
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
              break;
            case "verifyVendorAccess":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              ) {
                component.set(
                  "v.bidRecordId",
                  component.get("v.optionRecordId")
                );
                component.set("v.optionRecordId", returnValue.optionRecordId);
                component.set("v.productionSelected", returnValue.productionId);
                component.set("v.productionName", returnValue.productionName);
                component.set(
                  "v.productionOfficePreference",
                  returnValue.productionOfficePreference
                );
                if (component.get("v.typeOfService") == "optionsHousing")
                  component.set("v.mainContent", "bidVendorHousing");
                if (component.get("v.typeOfService") == "optionsGT")
                  component.set("v.mainContent", "bidVendorGround");
                if (returnValue.hasOwnProperty("productionAssocUserName"))
                  component.set(
                    "v.productionAssocUserName",
                    returnValue.productionAssocUserName
                  );
                if (returnValue.hasOwnProperty("productionAssocUserPhone"))
                  component.set(
                    "v.productionAssocUserPhone",
                    returnValue.productionAssocUserPhone
                  );
                if (returnValue.hasOwnProperty("productionAssocUserEmail"))
                  component.set(
                    "v.productionAssocUserEmail",
                    returnValue.productionAssocUserEmail
                  );
                if (returnValue.hasOwnProperty("productionAssocRole"))
                  component.set(
                    "v.productionAssocRole",
                    returnValue.productionAssocRole
                  );
              } else
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
              break;
            case "getCloseOutHousing":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              )
                component.set("v.closeOutData", returnValue);
              else {
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
                component.set("v.mainContent", "dashboardBids");
              }
              break;
            case "upsertCloseOutHousing":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Thank you!."
                });
                toastEvent.fire();
                component.set("v.mainContent", "dashboardBids");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;

              case "updateVATData":
                if (returnValue == "done") {
                  var toastEvent = $A.get("e.force:showToast");
                  toastEvent.setParams({
                    type: "success",
                    message: "Thank you!."
                  });
                  toastEvent.fire();
                } else {
                  var toastEvent = $A.get("e.force:showToast");
                  toastEvent.setParams({
                    type: "error",
                    message:
                      "Something went wrong. Please refresh the page and try again."
                  });
                  toastEvent.fire();
                }
                break;
            case "getVendorProfile":
            case "updateVendorProfile":
            case "getVendorContacts":
            case "upsertVendorContact":
            case "getPropertyProfile":
            case "updatePropertyProfile":
            case "getPropertyInRoom":
            case "updatePropertyInRoom":
            case "getPropertyOnSite":
            case "updatePropertyOnSite":
            case "getFleetCoach":
            case "upsertVendorVehicle":
            case "getFleetChauffeured":
            case "updateFleetChauffeured":
            case "getFleetRental":
            case "updateFleetRental":
            case "updateFleetCoach":
            case "getVendorPayment":
            case "updateVendorPayment":
              component.set("v.vendorData", returnValue);
              break;
            case "updateVendorHousingBid":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your bid has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "vendor");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "updateVendorGroundBid":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your bid has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "vendor");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "deleteVendorContact":
              if (returnValue.isDeleted)
                component.set("v.vendorData", returnValue.records);
              else
                self.showMessage(
                  "error",
                  "Action denied!",
                  "The contact is linked to a community user, and it cannot be deleted. Please contact the Road Rebel team."
                );
              break;
            case "deleteVendorVehicle":
              if (returnValue.isDeleted)
                component.set("v.vendorData", returnValue.records);
              else
                self.showMessage(
                  "error",
                  "Action denied!",
                  "We had a problem deleting this record. Please contact the Road Rebel team."
                );
              break;
            case "getProductions":
              component.set("v.productions", returnValue);
              break;
            case "createProduction":
              self.showMessage(
                "success",
                "Done!",
                "'" + returnValue + "' has been created."
              );
              component.set("v.mainContent", "dashboard");
              break;
            case "getProductionItineraries":
              component.set("v.productionName", returnValue.productionName);
              component.set(
                "v.productionCompany",
                returnValue.productionCompany
              );
              component.set("v.itineraries", returnValue.itineraries);
              break;
            case "getMultipleOptions":
              var lodgingRecords = JSON.parse(
                JSON.stringify(returnValue.lodgingRecords)
              );
              component.set("v.lodgingRecords", lodgingRecords);
              break;
            case "getProductionServices":
              component.set("v.menuSelected", "services");
              var itineraryData = component.get("v.itineraryData");
              component.set(
                "v.productionOfficePreference",
                returnValue.productionOfficePreference
              );
              itineraryData.services = returnValue.services;
              itineraryData.isLodgingLocked = returnValue.isLodgingLocked;
              itineraryData.isGroundLocked = returnValue.isGroundLocked;
              itineraryData.isAirLocked = returnValue.isAirLocked;
              itineraryData.isFreightLocked = returnValue.isFreightLocked;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getLodgingPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForHousing"))
                itineraryData.salesForHousing = returnValue.salesForHousing;
              if (returnValue.hasOwnProperty("salesHousingRoomTypes"))
                itineraryData.salesHousingRoomTypes =
                  returnValue.salesHousingRoomTypes;
              if (returnValue.hasOwnProperty("salesHousingConcessions"))
                itineraryData.salesHousingConcessions =
                  returnValue.salesHousingConcessions;
              if (returnValue.hasOwnProperty("lodgingRecords"))
                itineraryData.lodgingRecords = returnValue.lodgingRecords;
              else itineraryData.lodgingRecords = [];
              console.log("itineraryData :: " + itineraryData);
              itineraryData.concessionRecords =
                returnValue.salesHousingConcessions;
              itineraryData.distanceFromEventOptions =
                returnValue.distanceFromEventOptions;
              itineraryData.hotelStars = returnValue.hotelStars;
              itineraryData.hotelTypes = returnValue.hotelTypes;
              itineraryData.preferredBrands = returnValue.preferredBrands;
              itineraryData.roomTypes = returnValue.roomTypes;
              itineraryData.concessionHousingTypes =
                returnValue.concessionHousingTypes;
              itineraryData.concessionCorporateTypes =
                returnValue.concessionCorporateTypes;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getGroundPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForGround"))
                itineraryData.salesForGround = returnValue.salesForGround;
              if (returnValue.hasOwnProperty("groundRecords"))
                itineraryData.groundRecords = returnValue.groundRecords;
              else itineraryData.groundRecords = [];
              itineraryData.tripTypesGround = returnValue.tripTypesGround;
              itineraryData.locationPickUpTypes =
                returnValue.locationPickUpTypes;
              itineraryData.locationDropOffTypes =
                returnValue.locationDropOffTypes;
              itineraryData.vehicleTypesGround = returnValue.vehicleTypesGround;
              itineraryData.groupTypesGround = returnValue.groupTypesGround;
              itineraryData.amenitiesGround = returnValue.amenitiesGround;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getAirPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForAir"))
                itineraryData.salesForGround = returnValue.salesForAir;
              if (returnValue.hasOwnProperty("flightRecords"))
                itineraryData.flightRecords = returnValue.flightRecords;
              else itineraryData.flightRecords = [];
              itineraryData.classServicesAir = returnValue.classServicesAir;
              itineraryData.preferredAirlinesAir =
                returnValue.preferredAirlinesAir;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getFreightPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForFreight"))
                itineraryData.salesForGround = returnValue.salesForFreight;
              if (returnValue.hasOwnProperty("freightRecords"))
                itineraryData.freightRecords = returnValue.freightRecords;
              else itineraryData.freightRecords = [];
              itineraryData.groupTypesFreight = returnValue.groupTypesFreight;
              component.set("v.itineraryData", itineraryData);
              break;
            case "saveProductionServices":
              var firstService = returnValue.split(";")[0];
              if (firstService == "Housing")
                component.set("v.menuSelected", "housing");
              if (firstService == "Ground Travel")
                component.set("v.menuSelected", "ground");
              if (firstService == "Air") component.set("v.menuSelected", "air");
              if (firstService == "Freight")
                component.set("v.menuSelected", "freight");
              var itineraryData = component.get("v.itineraryData");
              itineraryData.services = returnValue;
              component.set("v.itineraryData", itineraryData);
              break;
            case "upsertItineraryRecord":
              var callToChild = $A.get("e.c:VoyajerCallToChild");
              if (returnValue.hasOwnProperty("errorMessage")) {
                callToChild.setParams({
                  action: returnValue.errorMessage,
                  data: {}
                });
              } else {
                var data = { record: returnValue.record };
                if (returnValue.hasOwnProperty("salesForHousing"))
                  data.salesForHousing = returnValue.salesForHousing;
                if (returnValue.hasOwnProperty("salesHousingRoomTypes"))
                  data.salesHousingRoomTypes =
                    returnValue.salesHousingRoomTypes;
                if (returnValue.hasOwnProperty("salesHousingConcessions"))
                  data.salesHousingConcessions =
                    returnValue.salesHousingConcessions;
                if (returnValue.hasOwnProperty("salesForGround"))
                  data.salesForGround = returnValue.salesForGround;
                callToChild.setParams({
                  action: returnValue.action,
                  data: data
                });
              }
              callToChild.fire();
              break;
            case "deleteItineraryRecord":
              var callToChild = $A.get("e.c:VoyajerCallToChild");
              if (returnValue.hasOwnProperty("errorMessage")) {
                callToChild.setParams({
                  action: returnValue.errorMessage,
                  data: {}
                });
              } else {
                callToChild.setParams({
                  action: returnValue.action,
                  data: {}
                });
              }
              callToChild.fire();
              break;
            case "subimtProductionItineraries":
              if (returnValue) {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your itinerary has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "dashboard");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "updateUserName":
              var client = component.get("v.client");
              client.userInfo = returnValue;
              component.set("v.client", client);
              self.showMessage(
                "success",
                "Done!",
                "Your profile has been updated."
              );
              break;
            case "saveLodgingPreferences":
              var client = component.get("v.client");
              client.preferencesSelected = returnValue;
              component.set("v.client", client);
              self.showMessage(
                "success",
                "Done!",
                "Your Lodging preferences has been updated."
              );
              break;
            case "getOptionsHousing":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              if (returnValue.serviceData.communityNoteAvailable === true) {
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }

              break;
            case "getOptionsHousingPreview":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              component.set("v.officePreference",returnValue.userInfo.Housing_Preference__c);
              console.log('returnValue.userInfo.Housing_Preference__c :: ' + returnValue.userInfo.Housing_Preference__c);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              if (returnValue.serviceData.communityNoteAvailable === true) {
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              break;
            case "getOptionsHousingDetail":
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getOptionsGT":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getOptionsGTDetail":
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getOptionsAir":
              console.log("inside GT getter");
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              console.log("communityNotes" + component.get("v.communityNotes"));
              console.log(
                "showCommunityNote" + component.get("v.showCommunityNote")
              );
              console.log("attempting to add hide class");
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getOptionsAirPreview":
              console.log("inside GT getter");
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              console.log("attempting to add hide class");
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getCommunityNote":
              console.log(returnValue);
              let theResponse = returnValue;
              if (theResponse != "") {
                component.set("v.communityNote", returnValue);
                component.set("v.openSelectOptionsAlert", true);
              }
              break;
            case "showMessages":
              component.set("v.openSelectOptionsAlert", true);
            case "submitBidSelected":
              var result = returnValue;
              if (returnValue == "done") {
                self.showMessage(
                  "success",
                  "Done!",
                  "The option has been selected."
                );
                component.set("v.mainContent", "dashboard");
              } else
                self.showMessage(
                  "error",
                  "",
                  "Something went wrong. Please contact Road Rebel Support team."
                );
              break;
            case "getOptionsAirDetail":
              console.log(returnValue.optionDetailRecord);
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getVendorBids":
              component.set("v.bids", returnValue);
              break;
            case "getVendorProductionBids":
              component.set("v.productionName", returnValue.productionName);
              component.set(
                "v.productionCompany",
                returnValue.productionCompany
              );
              component.set(
                "v.productionAssocUserName",
                returnValue.productionAssocUserName
              );
              component.set(
                "v.productionAssocUserPhone",
                returnValue.productionAssocUserPhone
              );
              component.set(
                "v.productionAssocUserEmail",
                returnValue.productionAssocUserEmail
              );
              component.set(
                "v.productionAssocRole",
                returnValue.productionAssocRole
              );
              component.set("v.itineraries", returnValue.itineraries);
              break;
            case "getReservationHousingDetail":
              component.set(
                "v.reservationDetail",
                returnValue.reservationDetailRecord
              );
              console.log("getReservationHousingDetail");
              console.log(returnValue.reservationDetailRecord);
              break;
            case "getReservationGTDetail":
              component.set(
                "v.reservationDetail",
                returnValue.reservationDetailRecord
              );
              console.log("getReservationGTDetail");
              console.log(returnValue.reservationDetailRecord);
              break;
            case "getContactUsData":
              component.set("v.contactUsData", returnValue);
              console.log(
                "getContactUsData - returnValue = " +
                  JSON.stringify(returnValue)
              );
              break;
            case "getDocuments":
              component.set("v.lsDocuments", returnValue.lsDocuments);
              component.set("v.lsDocumentsAux", returnValue.lsDocuments);
              break;
            case "saveDocument":
              console.log(returnValue);
              console.log("saveDocument success!");
              // self.showMessage("success","Done!","Your document has been successfully uploaded.");
              // call 'toastEvent' only work on one.app
              break;
            case "getVendorHousingBid":
            case "getVendorGroundBid":
              component.set(
                "v.productionOfficePreference",
                returnValue.productionOfficePreference
              );
              component.set("v.bidData", returnValue);
              break;
            case "unabledVendorBid":
              component.set("v.mainContent", "dashboardBids");
              self.showMessage("success", "", "Thanks for your answer.");
              break;
            default:
              alert(
                "Please add your method to the helper controller to know what to do with the response"
              );
              break;
          }
        } else if (state === "INCOMPLETE") {
          if (errors[0] && errors[0].message) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              title: "Internal Error",
              message: errors[0].message
            });
            toastEvent.fire();
          }
        } else if (state === "ERROR") {
          var errors = response.getError();
          if (errors) {
            if (errors[0] && errors[0].message) {
              var toastEvent = $A.get("e.force:showToast");
              toastEvent.setParams({
                type: "error",
                title: "Internal Error",
                message: errors[0].message
              });
              toastEvent.fire();
            }
          } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              title: "Internal Error",
              message: "Unknown error"
            });
            toastEvent.fire();
          }
        }
        $A.util.addClass(component.find("loadingPage"), "slds-hide");
      })
    );
    $A.enqueueAction(action);
    //$A.util.addClass(component.find("loadingPage"), "slds-hide");
  },
  getCloseOutRevenue: function (component) {
      var data = {};
      data.serviceId = component.get("v.serviceId");
      data.accountId = component.get("v.client").userInfo.Contact.AccountId;
      var action = component.get("c.getCloseOutHousingVAT");
      action.setParams({ data: JSON.stringify(data) });
      action.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                component.set("v.revenueVatData", response.getReturnValue());
                //alert("From server: " + response.getReturnValue());
            } else if (state === "ERROR") {
                var errors = response.getError();
                if (errors) {
                    if (errors[0] && errors[0].message) {
                        console.log("Error message: " + 
                                 errors[0].message);
                    }
                } else {
                    console.log("Unknown error");
                }
            }
        });
        $A.enqueueAction(action);
  },
  updateRevenue: function (component, data) {
      var action = component.get("c.updateVATDetails");
      action.setParams({ data: JSON.stringify(data) });
      action.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                //component.set("v.revenueVatData", response.getReturnValue());
                //alert("From server: " + response.getReturnValue());
            } else if (state === "ERROR") {
                var errors = response.getError();
                if (errors) {
                    if (errors[0] && errors[0].message) {
                        console.log("Error message: " + 
                                 errors[0].message);
                    }
                } else {
                    console.log("Unknown error");
                }
            }
        });
        $A.enqueueAction(action);
  },
  showMessage: function (type, title, message) {
    var toastEvent = $A.get("e.force:showToast");
    toastEvent.setParams({
      type: type,
      title: title,
      message: message
    });
    toastEvent.fire();
  }
});
```
### VoyajerController

```
({
	doInit: function (component, event, helper) {
		//helper.checkCommunityNote(component, event, helper);
		var urlString = window.location.href;
		var baseURL = urlString.substring(0, urlString.indexOf("/s"));
		component.set("v.sitePrefix", baseURL);

		var sPageURL = decodeURIComponent(window.location.search.substring(1)),
			sURLVariables = sPageURL.split("&"),
			sParameterName,
			hco = "",
			service = "",
			optionRecordId = "",
			stayId = "",
			i;
		for (i = 0; i < sURLVariables.length; i++) {
			sParameterName = sURLVariables[i].split("=");
			if (sParameterName[0] === "hco") hco = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "service") service = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "stayId") stayId = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "record") optionRecordId = sParameterName[1] === undefined ? "" : sParameterName[1];
		}
		component.set("v.hco", hco);
		optionRecordId = optionRecordId.trim();
		if (optionRecordId.length === 18 && !!optionRecordId) {
			switch (service) {
				case "lodging":
					service = "optionsHousing";
					break;
				case "ground":
					service = "optionsGT";
					break;
				case "freight":
					service = "optionsFreight";
					break;
				case "air":
					service = "optionsAir";
					break;
				default:
					service = "";
					optionRecordId = "";
					break;
			}
		} else {
			service = "";
			optionRecordId = "";
		}
		component.set("v.typeOfService", service);
		component.set("v.optionRecordId", optionRecordId);
		helper.crud(component, "getClient", {});
	},

	loadJquery: function (component, event, helper) {
		jQuery(document).ready(function () {});
	},

	loadDashboardContent: function (component, event, helper) {
		component.set("v.productionSelected", "");
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access this dashboard page.",
				});
				toastEvent.fire();
				break;
			case "Customer":
				component.set("v.mainContent", "dashboard");
				break;
			default:
				component.set("v.mainContent", "dashboardBids");
				break;
		}
	},

	loadReportsContent: function (component, event, helper) {
		component.set("v.productionSelected", "");
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access to this page.",
				});
				toastEvent.fire();
				break;
			default:
				component.set("v.mainContent", "reports");
				break;
		}
	},

	loadContactUsContent: function (component, event, helper) {
		component.set("v.mainContent", "contactus");
	},

	loadUserContent: function (component, event, helper) {
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access to this page.",
				});
				toastEvent.fire();
				break;
			case "Customer":
				component.set("v.mainContent", "user");
				$A.util.removeClass(component.find("loadingPage"), "slds-hide");
				break;
			default:
				component.set("v.mainContent", "vendor");
				break;
		}
	},

	logout: function (component, event, helper) {
		component.set("v.mainContent", "logout");
		window.location.replace(component.get("v.sitePrefix") + "/secur/logout.jsp");
	},

	handleCommunicationEvent: function (component, event, helper) {
		var data = {};
		console.log("case: " + event.getParam("action"));
		switch (event.getParam("action")) {
			case "refreshBidsSelected":
				var bidsSelected = event.getParam("data");
				component.set("v.bidsSelected", bidsSelected);
			case "updateVATAddressData":
				data = event.getParam("data");
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "updateVATData", data);
				break;
			case "loadProductions":
				setTimeout($A.getCallback(helper.crud.bind(this, component, "getProductions", data)), 0);
				break;
			case "showMessages":
				component.set("v.openSelectOptionsAlert", true);
				break;
			case "showDashboard":
				component.set("v.mainContent", "dashboard");
				break;
			case "newProduction":
				data.Name = event.getParam("data").productionName;
				data.CloseDate = event.getParam("data").startDate;
				data.ContactId = component.get("v.client").userInfo.ContactId;
				data.AccountId = component.get("v.client").userInfo.Contact.AccountId;
				data.officePreference = component.get("v.officePreference");
				helper.crud(component, "createProduction", data);
				break;
			case "loadItineraries":
				helper.crud(component, "getProductionItineraries", data);
				break;
			case "loadProductionServices":
				helper.crud(component, "getProductionServices", data);
				break;
			case "loadMultipleOptions":
				helper.crud(component, "getMultipleOptions", data);
				break;
			case "loadLodgingPage":
				helper.crud(component, "getLodgingPage", data);
				break;
			case "loadGroundPage":
				helper.crud(component, "getGroundPage", data);
				break;
			case "loadAirPage":
				helper.crud(component, "getAirPage", data);
				break;
			case "loadFreightPage":
				helper.crud(component, "getFreightPage", data);
				break;
			case "saveServices":
				data.productionId = event.getParam("data").productionId;
				data.services = event.getParam("data").services;
				helper.crud(component, "saveProductionServices", data);
				break;
			case "saveItineraryRecord":
				data.productionId = component.get("v.productionSelected");
				data.recordType = event.getParam("data").recordType;
				data.record = JSON.parse(JSON.stringify(event.getParam("data").record));
				data.officePreference = component.get("v.productionOfficePreference");
				helper.crud(component, "upsertItineraryRecord", data);
				break;
			case "removeItineraryRecord":
				data.productionId = component.get("v.productionSelected");
				data.recordType = event.getParam("data").recordType;
				data.recordId = event.getParam("data").recordId;
				helper.crud(component, "deleteItineraryRecord", data);
				break;
			case "submitItineraries":
				helper.crud(component, "subimtProductionItineraries", data);
				break;
			case "contentLoaded":
				$A.util.addClass(component.find("loadingPage"), "slds-hide");
				break;
			case "updatingUser":
				$A.util.removeClass(component.find("loadingPage"), "slds-hide");
				break;
			case "refreshUser":
				helper.crud(component, "updateUserName", data);
				break;
			case "updatePassword":
				console.log(event.getParam("data").currentPassword);
				console.log(event.getParam("data").newPassword);
				console.log(event.getParam("data").confirmPassword);
				break;
			case "savePreferences":
				helper.crud(component, "saveLodgingPreferences", data);
				break;
			case "loadOptionsHousing":
				helper.crud(component, "getOptionsHousing", data);
				break;
			case "loadOptionsHousingPreview":
				helper.crud(component, "getOptionsHousingPreview", data);
				break;
			case "loadOptionsHousingDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsHousingDetail", data);
				break;
			case "loadOptionsGT":
				helper.crud(component, "getOptionsGT", data);
				break;
			case "loadOptionsGTDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsGTDetail", data);
				break;
			case "loadOptionsAir":
				helper.crud(component, "getOptionsAir", data);
				break;
			case "loadOptionsAirPreview":
				helper.crud(component, "getOptionsAirPreview", data);
				break;
			case "loadOptionsAirDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsAirDetail", data);
				break;
			case "loadOptionsAirReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsAirDetail", data);
				break;
			case "loadOptionsHousingReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsHousingDetail", data);
				break;
			case "submitOptionSelected":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.productionId = component.get("v.productionSelected");
				data.contactName = component.get("v.client").userInfo.Contact.Name;
				var productions = component.get("v.productions");
				productions.forEach(production => {
					if (production.recordId == data.productionId) data.productionRecordTypeName = production.recordTypeName;
				});
				helper.crud(component, "submitBidSelected", data);
				break;
			case "changeMultipleOptions":
				/* using prefix of change for events fired on changes that aren't crud */
				/* data should have been sent for the VoyajerOptionsReviewSubmitItem insance that was edited */
				let allData = event.getParam("data");
				var theOptionIndex = allData.optionIndex;
				var theOptionData = allData.optionData;
				var theOptionComment = allData.optionComment;

				console.log('theOptionIndex:: ' + theOptionIndex);

				let currentBidOptions = component.get('v.theSelectedBidOptions');

				if (currentBidOptions.length === 0){
					console.log('current length 0');
					let bidOp = new Object();
					bidOp.record = theOptionData.record;
					bidOp.theOptionData = theOptionData;
					bidOp.theOptionIndex = theOptionIndex;
					bidOp.theOptionComment = theOptionComment;
					currentBidOptions.push(bidOp);  
				} else {
					console.log('current length not 0');
					if (currentBidOptions.hasOwnProperty(theOptionIndex)) {
						console.log('current length checking property exists - it does');

						currentBidOptions.forEach(bid => {
							if (bid.theOptionIndex === theOptionIndex) {
								console.log('theOptionIndex :: ' + theOptionIndex);
								console.log('bid theOptionIndex:: ' + bid.theOptionIndex);
								bid.record = theOptionData.record;
								bid.theOptionData = theOptionData;
								bid.theOptionIndex = theOptionIndex;
								bid.theOptionComment = theOptionComment;
							}
						});	
						console.log('updated comment');
					} else {
							let bidOp = new Object();
							bidOp.record = theOptionData.record;
							bidOp.theOptionData = theOptionData;
							bidOp.theOptionIndex = theOptionIndex;
							bidOp.theOptionComment = theOptionComment;
							currentBidOptions.push(bidOp);  
					}
				}

				/* this should be coming over to the helper as a list of bidoptions. */
				console.log('new currentBidOptions lengthh :: ' + currentBidOptions.length);	
				component.set("v.theSelectedBidOptions", currentBidOptions);
				break;
			case "submitMultipleOptionsSelected":
                //Fix By Clay Dev 20 March, 2021 #177292637
                component.set("v.theSelectedBidOptions", event.getParam("data").submittedBids);
				helper.crud(component, "saveMultipleOptionsSelected", data);
				break;
			case "loadOptionsGTReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsGTDetail", data);
				break;
			case "loadOptionsHousingCompare":
				data.compareList = event.getParam("data").compareList;
				break;
			case "loadOptionsGTCompare":
				data.compareList = event.getParam("data").compareList;
				break;
			case "loadVendorBids":
				setTimeout($A.getCallback(helper.crud.bind(this, component, "getVendorBids", data)), 0);
				break;
			case "loadVendorProductionBids":
				helper.crud(component, "getVendorProductionBids", data);
				break;
			case "loadReservationHousingDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getReservationHousingDetail", data);
				break;
			case "loadReservationGTDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getReservationGTDetail", data);
				break;
			case "loadContactUsData":
				//data.productionId = event.getParam("data").productionId;
				data.productionId = component.get("v.productionSelected");
				helper.crud(component, "getContactUsData", data);
				break;
			case "loadDocuments":
				data.serviceId = event.getParam("data").serviceId;
				helper.crud(component, "getDocuments", data);
				break;
			case "uploadDocument":
				data.docName = event.getParam("data").docName;
				data.docContentBase64 = event.getParam("data").docContentBase64;
				data.docReName = event.getParam("data").docReName;
				data.docType = event.getParam("data").docType;
				data.docServiceId = event.getParam("data").docServiceId;
				helper.crud(component, "saveDocument", data);
				data.serviceId = event.getParam("data").docServiceId;
				helper.crud(component, "getDocuments", data);
				break;
			case "loadCloseOut":
				data.serviceId = component.get("v.serviceId");
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "getCloseOutHousing", data);
				break;
			case "saveCloseOut":
				helper.crud(component, "upsertCloseOutHousing", JSON.parse(JSON.stringify(event.getParam("data"))));
				break;
			case "loadVendorProfile":
				helper.crud(component, "getVendorProfile", data);
				break;
			case "saveVendorProfile":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorProfile", data);
				break;
			case "loadVendorContacts":
				helper.crud(component, "getVendorContacts", data);
				break;
			case "saveVendorContact":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "upsertVendorContact", data);
				break;
			case "removeContact":
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				data.recordId = event.getParam("data");
				helper.crud(component, "deleteVendorContact", data);
				break;
			case "loadPropertyProfile":
				helper.crud(component, "getPropertyProfile", data);
				break;
			case "savePropertyProfile":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyProfile", data);
				break;
			case "loadPropertyInRoom":
				helper.crud(component, "getPropertyInRoom", data);
				break;
			case "savePropertyInRoom":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyInRoom", data);
				break;
			case "loadPropertyOnSite":
				helper.crud(component, "getPropertyOnSite", data);
				break;
			case "savePropertyOnSite":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyOnSite", data);
				break;
			case "loadFleetCoach":
				helper.crud(component, "getFleetCoach", data);
				break;
			case "saveVendorVehicle":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "upsertVendorVehicle", data);
				break;
			case "removeVehicle":
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				data.recordId = event.getParam("data");
				helper.crud(component, "deleteVendorVehicle", data);
				break;
			case "saveFleetCoach":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetCoach", data);
				break;
			case "loadFleetChauffeured":
				helper.crud(component, "getFleetChauffeured", data);
				break;
			case "saveFleetChauffeured":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetChauffeured", data);
				break;
			case "loadFleetRental":
				helper.crud(component, "getFleetRental", data);
				break;
			case "saveFleetRental":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetRental", data);
				break;
			case "loadPayment":
				helper.crud(component, "getVendorPayment", data);
				break;
			case "saveVendorPayment":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorPayment", data);
				break;
			case "loadVendorHousingBid":
				helper.crud(component, "getVendorHousingBid", data);
				break;
			case "placeHousingBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorHousingBid", data);
				break;
			case "placeGroundBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorGroundBid", data);
				break;
			case "loadVendorGroundBid":
				helper.crud(component, "getVendorGroundBid", data);
				break;
			case "unableToBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "unabledVendorBid", data);
				break;
			case "testCommunication":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				console.log(data);
				break;
			default:
				//alert("Please add your call to the controller");
				break;
		}
	},
});
```
### Voyajer

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### Voyajer

```
<aura:component
  implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction"
  access="global"
  controller="VoyajerController"
>
  <ltng:require styles="{!$Resource.RoadRebelUtils+'/css/all.css'}" />
  <ltng:require
    scripts="{!$Resource.RoadRebelUtils+'/js/jquery-3.3.1.min.js'}"
    afterScriptsLoaded="{!c.loadJquery}"
  />
  <aura:attribute
    type="VoyajerController.Client"
    name="client"
    default="{ userInfo: {}, preferencesAvailable: [], preferencesSelected: []}"
  />
  <aura:attribute
  type="Object[]"
  name="theSelectedBidOptions"
  default="[]"
/>       

  <aura:attribute
    type="Boolean"
    name="openSelectOptionsAlert"
    default="false"
  />
  <aura:attribute type="String" name="communityNotes" default="" />
  <aura:attribute type="String" name="modalTitle" default="" />
  <aura:attribute type="Boolean" name="showCommunityNote" default="false" />
  <aura:attribute type="List" name="productions" default="[]" />
  <aura:attribute type="List" name="theSelectedBids" default="[]" />
  <aura:attribute type="List" name="bidOptions" default="[]" />
  <aura:attribute type="List" name="compareList" default="[]" />
  <aura:attribute type="List" name="itineraries" default="[]" />
  <aura:attribute type="List" name="countries" default="[]" />
  <aura:attribute type="List" name="bidsSelected" />
  <aura:attribute
    type="List"
    name="lodgingPreferencesAvailable"
    default="[{ label: 'Airports', value: 'Airports' }]"
  />
  <aura:attribute
    type="User"
    name="userLogged"
    default="{'sobjectType' : 'User'}"
  />
  <aura:attribute type="List" name="lsDocuments" default="[]" />
  <aura:attribute type="List" name="lodgingRecords" default="[]" />
  <aura:attribute type="List" name="lsDocumentsAux" default="[]" />
  <aura:attribute type="String" name="sitePrefix" default="" />
  <aura:attribute type="String" name="userProfile" default="Forbidden" />
  <aura:attribute type="String" name="userName" />
  <aura:attribute type="String" name="officePreference" default="RRU" />
  <aura:attribute type="String" name="productionOfficePreference" default="" />
  <aura:attribute type="String" name="hco" default="" />
  <aura:attribute type="String" name="productionName" />
  <aura:attribute type="String" name="productionCompany" />
  <aura:attribute type="String" name="mainContent" />
  <aura:attribute type="String" name="menuSelected" />
  <aura:attribute type="String" name="productionSelected" default="" />
  <aura:attribute type="String" name="optionRecordId" />
  <aura:attribute type="String" name="typeOfService" />
  <aura:attribute type="Object" name="itineraryData" />
  <aura:attribute type="Object" name="recordTypes" />
  <aura:attribute type="Object" name="serviceData" />
  <aura:attribute type="Object" name="optionDetailRecord" />
  <aura:attribute type="Object" name="closeOutData" />
  <aura:attribute type="Object" name="vendorData" />
  <aura:attribute type="Object" name="bidData" />
  <aura:attribute type="Integer" name="optionDetailRecordId" />
  <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
  <aura:attribute type="Integer" name="bidOptionsSize" />
  <aura:attribute type="String" name="serviceId" />
  <aura:attribute type="String" name="serviceType" />
  <aura:attribute type="String" name="serviceDateInAndOut" />
  <aura:attribute type="String" name="serviceCityName" />
  <aura:attribute type="String" name="productionAssocUserName" />
  <aura:attribute type="String" name="productionAssocUserPhone" />
  <aura:attribute type="String" name="productionAssocUserEmail" />
  <aura:attribute type="String" name="productionAssocRole" />
  <aura:attribute type="String" name="bidRecordId" />
  <aura:attribute type="Object" name="reservationDetail" />
  <aura:attribute type="List" name="bids" default="[]" />
  <aura:attribute type="String" name="bidName" />
  <aura:attribute type="Object" name="contactUsData" />
  <aura:attribute type="Object" name="revenueVatData" />
  <aura:attribute type="List" name="bidOptionsFiltered" default="[]" />
  <aura:attribute name="startDate" type="String" />
  <aura:attribute name="endDate" type="String" />
  <aura:attribute name="selectedLookupId" type="String" />
  <aura:attribute name="selectedPillText" type="String" />
  <aura:handler
    name="change"
    value="{!v.theSelectedBids}"
    action="{!c.handleChangeSelectedBids}"
  />

  <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
  <aura:handler
    name="callToParent"
    action="{!c.handleCommunicationEvent}"
    event="c:VoyajerCallToParent"
  />
  <aura:handler
    name="callToParentGetRevenue"
    action="{!c.handleCommunicationEventGetRevenue}"
    event="c:VoyajerCallToParentGetRevenue"
  />
  <aura:handler
    name="callToParentUpdateVAT"
    action="{!c.handleCommunicationEventUpdateVAT}"
    event="c:VoyajerCallToParentUpdateVAT"
  />
  <aura:registerEvent type="c:VoyajerCallToChild" name="callToChild" />
  <div class="box">
    <lightning:spinner
      aura:id="loadingPage"
      alternativeText="Loading"
      size="large"
    />
    <div class="topNavigator">
      <div class="logoNavigator">
        <img src="{!$Resource.CommunityImages+'/LogoRR.png'}" />
      </div>
      <div class="buttonsNavigator">
        <div
          class="centerDiv"
          onclick="{!c.loadDashboardContent}"
          style="
             {
              !v.maincontent=='dashboard'?'border-bottom: 0.25em solid #0065ff;': '';
            }
          "
        >
          <div class="hideOnMobile">Dashboard</div>
          <div class="showOnMobile">
            <lightning:icon
              iconName="utility:screen"
              alternativeText="Dash."
              size="small"
            />
          </div>
        </div>
        <!--<div class="centerDiv" onclick="{!c.loadReportsContent}" style="{!v.mainContent=='reports'? 'border-bottom: 0.25em solid #0065ff;':''}">-->
        <!--<div class="hideOnMobile">Reports</div>-->
        <!--<div class="showOnMobile"><lightning:icon iconName="utility:copy_to_clipboard" alternativeText="Rep." size="small" /></div>-->
        <!--</div>-->
        <!--<div class="centerDiv" onclick="{!c.loadContactUsContent}" style="{!v.productionSelected != '' ? (v.mainContent=='contactus'? 'border-bottom: 0.25em solid #0065ff;':'') : 'display:none;'}">
                    <div class="hideOnMobile">Contact Us</div>
                    <div class="showOnMobile"><lightning:icon iconName="utility:groups" alternativeText="Rep." size="small" /></div>
                </div>-->

        <aura:if isTrue="{!not(empty(v.contactUsData))}">
          <div
            class="centerDiv"
            onclick="{!c.loadContactUsContent}"
            style="{!v.productionSelected != '' ? (v.mainContent=='contactus'? 'border-bottom: 0.25em solid #0065ff;':'') : 'display:none;'}"
          >
            <div class="hideOnMobile">Contact Us</div>
            <div class="showOnMobile">
              <lightning:icon
                iconName="utility:groups"
                alternativeText="Rep."
                size="small"
              />
            </div>
          </div>
        </aura:if>
      </div>
      <div class="profileNavigator">
        <aura:if isTrue="{!v.client.userInfo.User_Profile__c!='Forbidden'}">
          <div class="greeting hideOnMobile">
            <span style="padding-right: 0.3em">Hello,</span>
            <aura:if isTrue="{!v.client.userInfo.User_Profile__c=='Customer'}">
              <a href="javascript:void(0);" onclick="{!c.loadUserContent}"
                >{!v.client.userInfo.Name}</a
              >
              <aura:set attribute="else">
                <a href="javascript:void(0);" onclick="{!c.loadUserContent}"
                  >{!v.client.userInfo.Contact.Account.Name}</a
                >
              </aura:set>
            </aura:if>
          </div>
          <div
            class="centerDiv"
            onclick="{!c.loadUserContent}"
            style="{!v.mainContent=='user' || v.mainContent=='vendor'? 'border-bottom: 0.25em solid #0065ff;':''}"
          >
            <lightning:avatar
              src="{!v.client.userInfo.SmallPhotoUrl}"
              variant="circle"
              initials="{!v.client.userInfo.Initials__c}"
              alternativeText="{!v.client.Name}"
            />
          </div>
          <div
            class="centerDiv"
            onclick="{!c.logout}"
            style="
               {
                !v.maincontent=='logout'?'border-bottom: 0.25em solid #0065ff;': '';
              }
            "
          >
            <lightning:avatar
              src=""
              fallbackIconName="utility:logout"
              variant="square"
              alternativeText="Log Out"
              class="logoutIcon"
            />
          </div>
        </aura:if>
      </div>
    </div>
    <div class="mainPageContainer">
      <aura:if isTrue="{!v.mainContent=='dashboard'}">
        <c:VoyajerDashboard
          userLogged="{!v.client.userInfo}"
          productions="{!v.productions}"
          mainContent="{!v.mainContent}"
          officePreference="{!v.officePreference}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          openSelectOptionsAlert="{!v.openSelectOptionsAlert}"
          communityNote="{!v.communityNote}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='actions'}">
        <c:VoyajerActions
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          itineraries="{!v.itineraries}"
          optionRecordId="{!v.optionRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='itinerary'}">
        <c:VoyajerItinerary
          mainContent="{!v.mainContent}"
          menuSelected="{!v.menuSelected}"
          productionSelected="{!v.productionSelected}"
          itineraryData="{!v.itineraryData}"
          recordTypes="{!v.recordTypes}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousing'}">
        <c:VoyajerOptionsHousing
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          userProfile="{!v.userProfile}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptions}"
          bidOptionsFiltered="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
          bidsSelected="{!v.bidsSelected}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}"                       
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"                  
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsSubmitMultiple'}">
        <c:VoyajerOptionsEventsSubmit
          mainContent="{!v.mainContent}"
          housingId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          officePreference="{!v.officePreference}"
          bidOptions="{!v.bidOptionsFiltered}"
          bidOptionsSize="{!v.bidOptionsSize}"
          itineraryData="{!v.itineraryData}"
          lodgingRecords="{!v.lodgingRecords}"
          bidsSelected="{!v.bidsSelected}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingDetail'}">
        <c:VoyajerOptionsHousingDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
          preferencesSelected="{!v.client.preferencesSelected}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingReviewSubmit'}">
        <c:VoyajerOptionsHousingReviewSubmit
          mainContent="{!v.mainContent}"
          housingId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          officePreference="{!v.officePreference}"
          bidOptions="{!v.bidOptionsFiltered}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsHousingCompare'}">
        <c:VoyajerOptionsHousingCompare
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          housingId="{!v.optionRecordId}"
          officePreference="{!v.officePreference}"
          serviceData="{!v.serviceData}"
          housingType="{!v.serviceData.recordType}"
          bidOptions="{!v.bidOptions}"
          compareList="{!v.compareList}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGT'}">
        <c:VoyajerOptionsGT
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTDetail'}">
        <c:VoyajerOptionsGTDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTCompare'}">
        <c:VoyajerOptionsGTCompare
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          compareList="{!v.compareList}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsGTReviewSubmit'}">
        <c:VoyajerOptionsGTReviewSubmit
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          groundId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsFreight'}">
        <c:VoyajerOptionsFreight
          mainContent="{!v.mainContent}"
          itinerarySelected="{!v.optionRecordId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAir'}">
        <c:VoyajerOptionsAir
          communityNotes="{!v.communityNotes}"
          showCommunityNote="{!v.showCommunityNote}"
          modalTitle="{!v.modalTitle}"
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
          compareList="{!v.compareList}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAirDetail'}">
        <c:VoyajerOptionsAirDetail
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          optionDetailRecord="{!v.optionDetailRecord}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='optionsAirReviewSubmit'}">
        <c:VoyajerOptionsAirReviewSubmit
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          airId="{!v.optionRecordId}"
          serviceData="{!v.serviceData}"
          bidOptions="{!v.bidOptions}"
          optionDetailRecordId="{!v.optionDetailRecordId}"
          optionDetailRecord="{!v.optionDetailRecord}"
          optionDetailRecordIdReal="{!v.optionDetailRecordIdReal}"
          bidOptionsSize="{!v.bidOptionsSize}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='overview'}">
        <c:VoyajerItineraryOverview
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          optionRecordId="{!v.optionRecordId}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}"                           
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"                           
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='documents'}">
        <c:VoyajerDocuments
          mainContent="{!v.mainContent}"
          userProfile="{!v.client.userInfo.User_Profile__c}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          productionName="{!v.productionName}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          lsDocuments="{!v.lsDocuments}"
          lsDocuments_org="{!v.lsDocumentsAux}"
          bidName="{!v.bidName}"
          startDate="{!v.startDate}" 
          endDate="{!v.endDate}" 
          selectedLookupId="{!v.selectedLookupId}" 
          selectedPillText="{!v.selectedPillText}"  
        ></c:VoyajerDocuments>
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='newProduction'}">
        <c:VoyajerNewProduction
          userLogged="{!v.client.userInfo}"
          mainContent="{!v.mainContent}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='reports'}">
        <c:VoyajerReports userLogged="{!v.client.userInfo}" />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='contactus'}">
        <c:VoyajerContactUs contactUsData="{!v.contactUsData}" />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='user'}">
        <c:VoyajerUser
          userLogged="{!v.client.userInfo}"
          lodgingPreferencesAvailable="{!v.client.preferencesAvailable}"
          lodgingPreferencesSelected="{!v.client.preferencesSelected}"
          countries="{!v.countries}"
          countryAndStates="{!v.client.countryAndStates}"
        />
      </aura:if>

      <aura:if isTrue="{!v.mainContent=='closeOutHousing'}">
        <c:VoyajerCloseOutHousing
          mainContent="{!v.mainContent}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
          productionSelected="{!v.productionSelected}"
          officePreference="{!v.officePreference}"
          closeOutData="{!v.closeOutData}"
          closeOutRevenue = "{!v.revenueVatData}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='dashboardBids'}">
        <c:VoyajerDashboardBids
          userProfile="{!v.client.userInfo.User_Profile__c}"
          userLogged="{!v.client.userInfo}"
          bids="{!v.bids}"
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          bidRecordId="{!v.bidRecordId}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendor'}">
        <c:VoyajerVendor
          userLogged="{!v.client.userInfo}"
          userProfile="{!v.userProfile}"
          vendorData="{!v.vendorData}"
          countries="{!v.countries}"
          countryAndStates="{!v.client.countryAndStates}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorActions'}">
        <c:VoyajerVendorActions
          mainContent="{!v.mainContent}"
          bidRecordId="{!v.bidRecordId}"
          productionName="{!v.productionName}"
          productionCompany="{!v.productionCompany}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
          itineraries="{!v.itineraries}"
          optionRecordId="{!v.optionRecordId}"
          serviceId="{!v.serviceId}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorReservationHousingDetails'}">
        <c:VoyajerVendorReservationHousing
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          optionRecordId="{!v.optionRecordId}"
          bidRecordId="{!v.bidRecordId}"
          reservationDetail="{!v.reservationDetail}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='vendorReservationGTDetails'}">
        <c:VoyajerVendorReservationGT
          mainContent="{!v.mainContent}"
          productionName="{!v.productionName}"
          bidRecordId="{!v.bidRecordId}"
          reservationDetail="{!v.reservationDetail}"
          serviceId="{!v.serviceId}"
          serviceType="{!v.serviceType}"
          serviceCityName="{!v.serviceCityName}"
          serviceDateInAndOut="{!v.serviceDateInAndOut}"
          bidName="{!v.bidName}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='bidVendorHousing'}">
        <c:VoyajerVendorHousingBid
          mainContent="{!v.mainContent}"
          userProfile="{!v.userProfile}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionOfficePreference="{!v.officePreference}"
          bidData="{!v.bidData}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
        />
      </aura:if>
      <aura:if isTrue="{!v.mainContent=='bidVendorGround'}">
        <c:VoyajerVendorGroundBid
          mainContent="{!v.mainContent}"
          productionSelected="{!v.productionSelected}"
          productionName="{!v.productionName}"
          productionOfficePreference="{!v.officePreference}"
          bidData="{!v.bidData}"
          productionAssocUserName="{!v.productionAssocUserName}"
          productionAssocUserPhone="{!v.productionAssocUserPhone}"
          productionAssocUserEmail="{!v.productionAssocUserEmail}"
          productionAssocRole="{!v.productionAssocRole}"
        />
      </aura:if>
    </div>
  </div>
</aura:component>
```
### Voyajer

```
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600&display=swap');

.THIS {
    display: flex;
    height: 100%;
    font-family: 'Poppins', sans-serif;
    flex-direction: column;
}

.THIS .showOnMobile,
.THIS .showOnTablet {
    display: none;
}

.THIS .hideOnTablet {
    display: inline-flex;
}

.THIS .hideOnMobile {
    display: block;
}

.THIS h1 {
    font-size: 1.5rem;
}

.THIS .titleIcon {
    padding-right: 0.5em;
    color: #606060;
}

.THIS .topNavigator {
    height: 4.375em;
    background-color: white;
    border-bottom: 1px solid #9f9f9f;
    display: flex;
    font-size: 0.75rem;
}

.THIS .logoNavigator {
    display: flex;
    height: 100%;
}

.THIS .logoNavigator > img {
    max-height: 100%;
    max-width: 100%;
}

.THIS .buttonsNavigator {
    align-items: center;
    display: flex;
    flex: 1;
    font-size: .75rem;
    font-weight: 500;
}

.THIS .profileNavigator,
.THIS .profileNavigator > div {
    padding: 0 0.5em;
    display: flex;
    align-items: center;
    justify-content: center;
}

.THIS .profileNavigator > div {
    height: 100%;
}

.THIS .centerDiv {
    align-items: center;
    justify-content: center;
    display: flex;
    height: 100%;
    margin-left: 1.5em;
    padding: 0 1em;
    border-bottom: 0.25em solid transparent;
    cursor: pointer;
}

.THIS .centerDiv:last-child {
    margin-right: 1.5em;
}

.THIS .centerDiv:hover {
    border-bottom: 0.25em solid #00b4ff;
}

.THIS .centerDiv > div {
    margin-top: 0.25em;
}

.THIS .logoutIcon .slds-icon {
    fill: #0065ff;
}

.THIS .profileNavigator .greeting {
    margin-right: -0.5em;
}

.THIS .profileNavigator .greeting > a {
    white-space: nowrap;
    max-width: 8em;
    overflow: hidden;
    text-overflow: ellipsis;
}

.THIS .mainPageContainer {
    background-color: #f0f0f0;
    display: flex;
    flex: 1;
    overflow-y: auto;
}

.THIS .mainPageContainer > div {
    display: flex;
    flex: 1;
    overflow-y: auto;
}

.THIS .mainMenu {
    background: #282828;
    color: white !important;
    float: left;
    height: 100%;
    overflow-y: auto;
    width: 15em;
    font-size: 0.75rem;
}

.THIS .sideBarProfile .slds-nav-vertical__item:hover::before {
    background: rgba(21, 137, 238, 0.25);
}

.THIS .sideBarProfile .slds-nav-vertical__action,
.THIS .sideBarItinerary .slds-nav-vertical__action {
    color: white !important;
    padding: 0.5em 1.25em;
}

.THIS .sideBarProfile .slds-nav-vertical__action:hover {
    box-shadow: #00b4ff 0.125rem 0px 0px inset;
}

.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarItinerary .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action:hover,
.THIS .sideBarItinerary .slds-is-active .slds-nav-vertical__action:hover {
    box-shadow: #00b4ff 0.25rem 0px 0px inset;
}

.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action,
.THIS .sideBarProfile .slds-is-active .slds-nav-vertical__action:hover {
    background: #0065ff;
}

.THIS .sideBarItinerary .slds-nav-vertical__item:hover::before {
    background: transparent;
}

.THIS .sideBarItinerary .slds-nav-vertical__action:hover {
    box-shadow: none;
}

.THIS .sideBarItinerary .slds-nav-vertical__action {
    cursor: default;
}

.THIS .sideBarItinerary .slds-nav-vertical__item.slds-is-active:hover:before {
    background: rgba(21, 137, 238, 0.1) !important;
}

.THIS .sideBarItinerary .slds-nav-vertical__action svg,
.THIS .sideBarProfile .slds-nav-vertical__action svg {
    fill: white !important;
}

.THIS .sideBarItineraryIcon {
    width: 1.5rem;
}

.THIS .checkpoint {
    position: absolute;
    right: 0;
    margin-right: 1em;
    color: #00b4ff;
    font-size: 1rem;
}

.THIS .checkpointIcon {
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.THIS .checkpointBackground {
    width: 0.65em;
    height: 0.65em;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
}

.THIS .pageContent {
    display: flex;
    flex: 1;
    flex-direction: column;
    overflow-y: auto;
    font-size: 0.875rem;
}

.THIS .pageContentSpaces {
    padding: 2em;
    max-width: 82em;
    width: 100%;
    margin: 0 auto;
}

.THIS .page-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5em;
}

.THIS .pageContent h1,
.THIS .pageContent h2 {
    flex: 1;
    font-size: 1.45rem;
    font-weight: 600;
}

.THIS .pageContent h1 {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.THIS .pageContent h2 {
    font-weight: 500;
}

.THIS .pageContent h3 {
    font-size: 1.25rem;
}

.THIS .page-section {
    display: flex;
    flex-direction: column;
}

.THIS .page-section-buttons {
    display: flex;
    justify-content: space-between;
    width: 100%;
    align-items: flex-end;;
}

.THIS .page-section-buttons > div {
    display: flex;
    margin-top: 0.5em;
}

.THIS .page-section-content_header {
    display: flex;
    text-align: center;
    padding: 2em 2em 0;
    flex-direction: column;
}

.THIS .page-section-content_center {
    text-align: center;
    display: flex;
    justify-content: center;
    flex-flow: wrap;
}

.THIS .page-section-services_center {
    text-align: center;
    display: flex;
    justify-content: space-evenly;
    flex-flow: wrap;
    max-width: 50em;
    width: 100%;
    margin: 1.5em 0;
}

.THIS .pageContentForm,
.THIS .pageContentDashboard {
    background-color: white;
    text-align: justify;
    padding: 2em;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
}

.THIS .pageContentForm p {
    line-height: 2;
    margin-bottom: 1em;
}

.THIS .pageContentForm p:last-child {
    margin-bottom: 0;
}

.THIS .pageContentDashboard {
    padding: 1em;
    font-size: 0.8rem;
}

.THIS .pageContentDashboardVendor {
    padding: 2em;
    font-size: 0.8rem;
}

.THIS .dashboardPill {
    width: 100%;
    color: #e00000;
}

.THIS .dashboardPill svg {
    fill: #e00000;
}

.THIS .dashboardPill .slds-pill__action {
    border: none;
}

.THIS .formColumnTwoChilds,
.THIS .formColumnThreeChilds,
.THIS .formColumnTwoChildsWithDate,
.THIS .formColumnThreeChildsDependant,
.THIS .formColumnFourChildsDependant {
    display: flex;
    width: 100%;
    min-width: 0;
}

.THIS .formColumnTwoChilds > *,
.THIS .formColumnThreeChilds > *,
.THIS .formColumnTwoChildsWithDate > * {
    width: 100%;
}

.THIS .formColumnTwoChildsWithDate > *:last-child {
    width: 60%;
}

.THIS .formColumnThreeChildsDependant > *:first-child,
.THIS .formColumnFourChildsDependant > *:first-child {
    width: auto;
    flex: 1;
}

.THIS .formColumnThreeChildsDependant > *:last-child {
    display: flex;
    flex: 2;
    flex-direction: column;
    margin-left: -1.5em;
}

.THIS .formColumnFourChildsDependant > *:last-child {
    display: flex;
    flex: 3;
    flex-direction: column;
    margin-left: -1.5em;
}

.THIS .formField {
    min-width: 0;
    width: 100%;
    padding: 0px 0.25rem;
    margin-bottom: 0.5rem;
}

.THIS .formFieldHorizontal {
    display: flex;
}

.THIS .formFieldHorizontal > .slds-form-element {
    flex: 1;
}

.THIS .formField label {
    overflow-wrap: break-word;
    display: inline-block;
    color: rgb(105, 105, 105);
    font-size: 1em;
    font-weight: 500;
    padding-right: 0.5rem;
    padding-top: 0.25rem;
    margin-bottom: 0.25rem;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.THIS .formField > label > span {
    font-size: 0.8em;
    font-weight: 400;
    padding-left: 0.75em;
}

.THIS .formColumnBlank {
    display: flex;
    width: 100%;
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

.THIS .slds-button {
    border-radius: 3em;
    text-transform: uppercase;
}

.THIS .formButtonBrand {
    background-color: #0065ff;
}

.THIS .formButtonBrand:hover,
.THIS .formButtonBrand:focus {
    background-color: #0051ce;
}

.THIS .formButtonBrandLight {
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .formButtonBrandLight:hover,
.THIS .formButtonBrandLight:focus {
    background-color: #009cf1;
    border-color: #00a4fb;
}

.THIS .formButtonBrandInverse {
    color: #0065ff;
    border-color: #0065ff;
}

.THIS .formButtonBrandInverse:hover,
.THIS .formButtonBrandInverse:focus {
    background-color: #dfebff;
}

.THIS .formButtonBrandInverse:focus {
    box-shadow: 0px 0px 2px 2px #afceff;
}

.THIS .formButtonDestructive {
    background-color: #e00000;
    color: white;
}

.THIS .formButtonDestructive:hover,
.THIS .formButtonDestructive:focus {
    background-color: #bf0000;
}

.THIS .formButtonDestructive:focus {
    box-shadow: 0px 0px 2px 2px #ff9b9b;
}

.THIS .formButtonDestructiveInverse {
    color: #e00000;
    border-color: #e00000;
}

.THIS .formButtonDestructiveInverse:hover,
.THIS .formButtonDestructiveInverse:focus {
    background-color: #ffeaea;
}

.THIS .formButtonDestructiveInverse:focus {
    box-shadow: 0px 0px 2px 2px #ff9b9b;
}

.THIS .formButtonSuccess {
    background-color: #17b216;
    color: white;
}

.THIS .formButtonSuccess:hover,
.THIS .formButtonSuccess:focus {
    background-color: #019a00;
}

.THIS .formButtonSuccess:focus {
    box-shadow: 0px 0px 2px 2px #17b216;
}

.THIS .formButtonAction {
    background-color: #ec4518;
    color: white;
    border-color: #ff3600;
}

.THIS .formButtonAction:hover,
.THIS .formButtonAction:focus {
    background-color: #e83100;
}

.THIS .formButtonAction:focus {
    box-shadow: 0px 0px 2px 2px #bf2900;
}

.THIS .clear {
    color: #e00000;
}

.THIS .page-section_record {
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    width: 100%;
    border: 1px solid #dbdbdb;
    margin: 0.5em 0 1em;
}

.THIS .page-section_record > div,
.THIS .page-section_record > div > div,
.THIS .recordDetails > div {
    display: flex;
}

.THIS .recordBodySideColumn {
    min-width: 3.25em;
    border-right: 1px solid #dbdbdb;
    justify-content: center;
    background-color: #f7f9fe;
    color: #9f9f9f;
    font-weight: 500;
    align-items: center;
}

.THIS .recordBodySideColumn span {
    font-size: 1.25em;
}

.THIS .recordHeader {
    height: 3.25em;
}

.THIS .recordTitle {
    padding: 0 1.5em;
}

.THIS .recordTitle,
.THIS .recordTitleText {
    align-items: center;
    flex: 1;
    overflow: hidden;
}

.THIS .recordTitle > div {
    align-items: center;
    display: flex;
    height: 100%;
}

.THIS .recordTitleText > div {
    font-weight: 500;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

.THIS .recordTitleText .location {
    color: #00b4ff;
    font-weight: 600;
}

.THIS .recordTitleText .dates {
    color: #606060;
    min-width: 10rem;
    text-align: left;
    padding-left: 0.5em;
    border-left: 2px solid #9f9f9f;
    margin-left: 0.5em;
}

.THIS .recordTitleButton {
    padding-left: 0.5em;
}

.THIS .recordBody {
    border-top: 1px solid #dbdbdb;
}

.THIS .recordBodyContent {
    display: flex;
    flex: 1;
    flex-direction: column;
    width: 100%;
    padding: 1.5em;
    min-width: 0;
}

.THIS .recordDetails {
    border: 1px solid #dbdbdb;
    margin-top: 1.5em;
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    width: 100%;
}

.THIS .recordDetails .recordTitle {
    background-color: #f0f0f0;
    height: 3.75em;
}

.THIS .recordDetails .recordBodyContent {
    border-top: 1px solid #dbdbdb;
}

.THIS .recordActions {
    margin-top: 1.5em;
}

.THIS .titleArrow {
    fill: white !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    display: block;
}

.THIS .tableRow > div > span {
    white-space: pre-wrap; /*update*/
}

.THIS .tableLocation {
    flex: 2;
}

.THIS .tableTripRow {
    display: flex;
    width: 100%;
    flex: 1;
    min-width: 0;
}

.THIS .tableTripRow > div {
    width: 100%;
}

.THIS .tripInfo {
    flex: 2;
}

.THIS .tabIcon {
    color: #606060;
    font-size: 1.25rem;
}

.THIS .buttonColumn {
    display: flex !important;
    width: 2em;
    padding: .25em 0 !important;
    align-items: flex-start;
    justify-content: flex-start;
}

@media (max-width: 1200px) {
    .THIS .showOnTablet {
        display: inline-flex !important;
    }
    
    .THIS .hideOnTablet {
        display: none !important;
    }
}

@media (max-width: 1024px) {
    .THIS .topNavigator {
        height: 3.5em;
    }
}

@media (max-width: 800px) {
    .THIS .pageContentSpaces {
        padding: 1.5em;
    }
    
    .THIS .pageContentForm {
        padding: 1em;
    }
    
    .THIS .page-section-buttons {
        flex-direction: column;
        width: 100%;
    }
    
    .THIS .page-section-buttons > div {
        width: 100%;
    }
}

@media (max-width: 550px) {
    .THIS .showOnMobile {
        display: block !important;
    }
    
    .THIS .hideOnMobile {
        display: none !important;
    }
    
    .THIS .mainMenu {
        width: 3.5em;
    }
    
    .THIS .pageContentSpaces {
        padding: 1em;
    }
    
    .THIS .formColumnThreeChildsDependant > *,
    .THIS .formColumnFourChildsDependant > * {
        width: 100%;
    }
    
    .THIS .page-section-buttons,
    .THIS .formColumnTwoChilds,
    .THIS .formColumnThreeChilds,
    .THIS .formColumnTwoChildsWithDate,
    .THIS .formColumnThreeChildsDependant,
    .THIS .formColumnFourChildsDependant {
        flex-wrap: wrap;
    }
    
    .THIS .formColumnThreeChildsDependant > *:last-child,
    .THIS .formColumnFourChildsDependant > *:last-child {
        flex-wrap: wrap;
        display: flex;
        flex-direction: column;
        margin-left: 0;
    }
    
    .THIS .page-section-buttons > div {
        justify-content: space-between;
    }
    
    .THIS .formColumnBlank {
        display: none;
    }
    
    .THIS .checkpoint {
        font-size: .75rem;
        top: 30%;
        right: 0;
    }
}

@media print {
    .THIS .mainPageContainer{
      overflow-y: unset !important;
    }
}
```
### VoyajerHelper

```
({
  checkCommunityNote: function (cmp) {
    var action = cmp.get("c.getCommunityNote");
    action.setParams({
      contactId: cmp.get("v.client").userInfo.ContactId,
      officePreference: cmp.get("v.officePreference")
    });
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var response = response.getReturnValue();
      })
    );
    $A.enqueueAction(action);
  },
  crud: function (component, methodName, data) {
    function alphanumeric(text) {
      if (typeof text !== "string") return false;
      if (!!text && text.length != 18) return false;
      for (var i = 0; i < text.length; i++) {
        var code = text.charCodeAt(i);
        if (
          !(code > 47 && code < 58) &&
          !(code > 64 && code < 91) &&
          !(code > 96 && code < 123)
        )
          return false;
      }
      return true;
    }
    var self = this;
    var action = component.get("c." + methodName);
    $A.util.removeClass(component.find("loadingPage"), "slds-hide");
    switch (methodName) {
      case "saveLodgingPreferences":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          preferences: component.get("v.client").preferencesSelected.join(";")
        });
        break;
      case "getProductions":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          officePreference: component.get("v.officePreference")
        });
        break;
      case "getCommunityNote":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId,
          officePreference: component.get("v.officePreference")
        });
        break;
      case "getVendorProfile":
      case "getPropertyProfile":
      case "getPropertyInRoom":
      case "getPropertyOnSite":
      case "getFleetCoach":
      case "getFleetChauffeured":
      case "getFleetRental":
      case "getVendorPayment":
        action.setParams({
          accountId: component.get("v.client").userInfo.Contact.AccountId
        });
        break;
      case "getProductionItineraries":
      case "getMultipleOptions":
        action.setParams({
          productionId: component.get("v.productionSelected"),
          productionOfficePreference: component.get(
            "v.productionOfficePreference"
          )
        });
      case "getProductionServices":
      case "subimtProductionItineraries":
        action.setParams({
          productionId: component.get("v.productionSelected")
        });
        break;
      case "getLodgingPage":
      case "getGroundPage":
      case "getAirPage":
      case "getFreightPage":
        action.setParams({
          productionId: component.get("v.productionSelected"),
          productionOfficePreference: component.get(
            "v.productionOfficePreference"
          )
        });
        break;
      case "getVendorProductionBids":
        action.setParams({ bidId: component.get("v.bidRecordId") });
        break;
      case "createProduction":
      case "saveProductionServices":
      case "upsertItineraryRecord":
      case "deleteItineraryRecord":
      case "getCloseOutHousing":
      case "upsertCloseOutHousing":
      case "submitBidSelected":
      case "updateVendorProfile":
      case "upsertVendorContact":
      case "updatePropertyProfile":
      case "updatePropertyInRoom":
      case "updatePropertyOnSite":
      case "upsertVendorVehicle":
      case "updateFleetCoach":
      case "updateFleetChauffeured":
      case "updateFleetRental":
      case "updateVendorPayment":
      case "updateVendorHousingBid":
      case "updateVendorGroundBid":
      case "unabledVendorBid":
        action.setParams({ data: JSON.stringify(data) });
        break;
      case "getOptionsHousing":
        action.setParams({ housingId: component.get("v.optionRecordId") });
        break;
      case "getOptionsHousingDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getOptionsGT":
        action.setParams({ groundId: component.get("v.optionRecordId") });
        break;
      case "getOptionsGTDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getOptionsAir":
        action.setParams({ airId: component.get("v.optionRecordId") });
        break;
      case "getOptionsAirDetail":
        action.setParams({ optionDetailRecordId: data.detailRecordId });
        break;
      case "getVendorBids":
        action.setParams({
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "getReservationHousingDetail":
        action.setParams({ bidRecordId: data.detailRecordId });
        break;
      case "getReservationGTDetail":
        action.setParams({ bidRecordId: data.detailRecordId });
        break;
      case "getContactUsData":
        action.setParams({
          productionId: component.get("v.productionSelected")
        });
        break;
      case "getDocuments":
        action.setParams({ serviceId: data.serviceId });
        break;
      case "saveDocument":
        action.setParams({
          fileName: data.docName,
          fileContentBase64: data.docContentBase64,
          fileReName: data.docReName,
          fileType: data.docType,
          entityId: data.docServiceId
        });
        break;
      case "getVendorContacts":
        action.setParams({
          accountId: component.get("v.client").userInfo.Contact.AccountId,
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "deleteVendorContact":
      case "deleteVendorVehicle":
        action.setParams({
          accountId: data.accountId,
          recordId: data.recordId
        });
        break;
      case "verifyOptionAccess":
        action.setParams({
          typeOfService: component.get("v.typeOfService"),
          optionRecordId: component.get("v.optionRecordId"),
          contactId: component.get("v.client").userInfo.ContactId
        });
        break;
      case "verifyVendorAccess":
        action.setParams({
          typeOfService: component.get("v.typeOfService"),
          optionRecordId: component.get("v.optionRecordId"),
          accountId: component.get("v.client").userInfo.Contact.AccountId
        });
        break;
      case "getVendorHousingBid":
      case "getVendorGroundBid":
        action.setParams({
          recordId: component.get("v.optionRecordId"),
          accountId: component.get("v.client").userInfo.Contact.AccountId,
          isRRE: component.get("v.officePreference") == "RRE" ? true : false
        });
        break;
      case "updateVATData":
        action.setParams({data: JSON.stringify(data)});
      case "saveMultipleOptionsSelected":
        let theBidOptions = [];
        theBidOptions = component.get('v.theSelectedBidOptions');
        action.setParams({bidData : theBidOptions});
        console.log('bidOptions length :: ' + theBidOptions.length);
        break;
      default:
        break;
    }
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var state = response.getState();
        if (state === "SUCCESS") {
          var returnValue = response.getReturnValue();
          let noteFixed = "";   
          switch (methodName) {
            case "saveMultipleOptionsSelected":
              self.showMessage("success","Done!","Your options have all been updated.");
              self.crud(component, "getOptionsHousing", {});
              component.set("v.mainContent","dashboard");
              break;
            case "getClient":
              component.set("v.client", returnValue);
              //this.checkCommunityNote(component);
              var countries = [];
              for (var country in returnValue.countryAndStates.pickListMap)
                countries.push(country);
              component.set("v.countries", countries);
              component.set("v.recordTypes", returnValue.recordTypes);
              console.log(returnValue.userInfo.User_Profile__c);
              if (returnValue.userInfo.hasOwnProperty("Housing_Preference__c"))
                component.set(
                  "v.officePreference",
                  returnValue.userInfo.Housing_Preference__c
                );
              if (
                returnValue.userInfo.hasOwnProperty("User_Profile__c") &&
                returnValue.userInfo.User_Profile__c != "Forbidden"
              ) {
                component.set(
                  "v.userProfile",
                  returnValue.userInfo.User_Profile__c
                );
                if (returnValue.userInfo.User_Profile__c == "Customer") {
                  if (!!component.get("v.optionRecordId"))
                    self.crud(component, "verifyOptionAccess", {});
                  component.set("v.mainContent", "dashboard");
                } else {
                  if (!!component.get("v.optionRecordId")) {
                    component.set("v.mainContent", "dashboardBids");
                    if (
                      (alphanumeric(component.get("v.optionRecordId")) &&
                        (component.get("v.userProfile") == "HousingVendor" ||
                          component.get("v.userProfile") ==
                            "CorporateVendor") &&
                        component.get("v.typeOfService") == "optionsHousing") ||
                      (component.get("v.userProfile") == "GroundVendor" &&
                        component.get("v.typeOfService") == "optionsGT")
                    )
                      self.crud(component, "verifyVendorAccess", {});
                    else
                      self.showMessage(
                        "error",
                        "",
                        "You have no access to this record. Please contact Road Rebel team for support."
                      );
                  } else if (!!component.get("v.hco")) {
                    if (!alphanumeric(component.get("v.hco")))
                      self.showMessage(
                        "error",
                        "",
                        "You have no access to this record. Please contact Road Rebel team for support."
                      );
                    else {
                      component.set("v.serviceId", component.get("v.hco"));
                      component.set("v.mainContent", "closeOutHousing");
                    }
                  } else component.set("v.mainContent", "dashboardBids");
                }
              } else
                self.showMessage(
                  "error",
                  "Your are not a community user!",
                  "Your have no access to this page."
                );
              self.crud(component, "getCommunityNote", {});
              break;
            case "verifyOptionAccess":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              ) {
                component.set("v.productionSelected", returnValue.productionId);
                component.set("v.productionName", returnValue.productionName);
                self.crud(component, "getContactUsData", {});
                component.set(
                  "v.mainContent",
                  component.get("v.typeOfService")
                );
              } else
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
              break;
            case "verifyVendorAccess":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              ) {
                component.set(
                  "v.bidRecordId",
                  component.get("v.optionRecordId")
                );
                component.set("v.optionRecordId", returnValue.optionRecordId);
                component.set("v.productionSelected", returnValue.productionId);
                component.set("v.productionName", returnValue.productionName);
                component.set(
                  "v.productionOfficePreference",
                  returnValue.productionOfficePreference
                );
                if (component.get("v.typeOfService") == "optionsHousing")
                  component.set("v.mainContent", "bidVendorHousing");
                if (component.get("v.typeOfService") == "optionsGT")
                  component.set("v.mainContent", "bidVendorGround");
                if (returnValue.hasOwnProperty("productionAssocUserName"))
                  component.set(
                    "v.productionAssocUserName",
                    returnValue.productionAssocUserName
                  );
                if (returnValue.hasOwnProperty("productionAssocUserPhone"))
                  component.set(
                    "v.productionAssocUserPhone",
                    returnValue.productionAssocUserPhone
                  );
                if (returnValue.hasOwnProperty("productionAssocUserEmail"))
                  component.set(
                    "v.productionAssocUserEmail",
                    returnValue.productionAssocUserEmail
                  );
                if (returnValue.hasOwnProperty("productionAssocRole"))
                  component.set(
                    "v.productionAssocRole",
                    returnValue.productionAssocRole
                  );
              } else
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
              break;
            case "getCloseOutHousing":
              if (
                returnValue.hasOwnProperty("isAccessible") &&
                returnValue.isAccessible
              )
                component.set("v.closeOutData", returnValue);
              else {
                self.showMessage(
                  "error",
                  "",
                  "You have no access to this record. Please contact Road Rebel team for support."
                );
                component.set("v.mainContent", "dashboardBids");
              }
              break;
            case "upsertCloseOutHousing":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Thank you!."
                });
                toastEvent.fire();
                component.set("v.mainContent", "dashboardBids");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;

              case "updateVATData":
                if (returnValue == "done") {
                  var toastEvent = $A.get("e.force:showToast");
                  toastEvent.setParams({
                    type: "success",
                    message: "Thank you!."
                  });
                  toastEvent.fire();
                } else {
                  var toastEvent = $A.get("e.force:showToast");
                  toastEvent.setParams({
                    type: "error",
                    message:
                      "Something went wrong. Please refresh the page and try again."
                  });
                  toastEvent.fire();
                }
                break;
            case "getVendorProfile":
            case "updateVendorProfile":
            case "getVendorContacts":
            case "upsertVendorContact":
            case "getPropertyProfile":
            case "updatePropertyProfile":
            case "getPropertyInRoom":
            case "updatePropertyInRoom":
            case "getPropertyOnSite":
            case "updatePropertyOnSite":
            case "getFleetCoach":
            case "upsertVendorVehicle":
            case "getFleetChauffeured":
            case "updateFleetChauffeured":
            case "getFleetRental":
            case "updateFleetRental":
            case "updateFleetCoach":
            case "getVendorPayment":
            case "updateVendorPayment":
              component.set("v.vendorData", returnValue);
              break;
            case "updateVendorHousingBid":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your bid has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "vendor");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "updateVendorGroundBid":
              if (returnValue == "done") {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your bid has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "vendor");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "deleteVendorContact":
              if (returnValue.isDeleted)
                component.set("v.vendorData", returnValue.records);
              else
                self.showMessage(
                  "error",
                  "Action denied!",
                  "The contact is linked to a community user, and it cannot be deleted. Please contact the Road Rebel team."
                );
              break;
            case "deleteVendorVehicle":
              if (returnValue.isDeleted)
                component.set("v.vendorData", returnValue.records);
              else
                self.showMessage(
                  "error",
                  "Action denied!",
                  "We had a problem deleting this record. Please contact the Road Rebel team."
                );
              break;
            case "getProductions":
              component.set("v.productions", returnValue);
              break;
            case "createProduction":
              self.showMessage(
                "success",
                "Done!",
                "'" + returnValue + "' has been created."
              );
              component.set("v.mainContent", "dashboard");
              break;
            case "getProductionItineraries":
              component.set("v.productionName", returnValue.productionName);
              component.set(
                "v.productionCompany",
                returnValue.productionCompany
              );
              component.set("v.itineraries", returnValue.itineraries);
              break;
            case "getMultipleOptions":
              var lodgingRecords = JSON.parse(
                JSON.stringify(returnValue.lodgingRecords)
              );
              component.set("v.lodgingRecords", lodgingRecords);
              break;
            case "getProductionServices":
              component.set("v.menuSelected", "services");
              var itineraryData = component.get("v.itineraryData");
              component.set(
                "v.productionOfficePreference",
                returnValue.productionOfficePreference
              );
              itineraryData.services = returnValue.services;
              itineraryData.isLodgingLocked = returnValue.isLodgingLocked;
              itineraryData.isGroundLocked = returnValue.isGroundLocked;
              itineraryData.isAirLocked = returnValue.isAirLocked;
              itineraryData.isFreightLocked = returnValue.isFreightLocked;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getLodgingPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForHousing"))
                itineraryData.salesForHousing = returnValue.salesForHousing;
              if (returnValue.hasOwnProperty("salesHousingRoomTypes"))
                itineraryData.salesHousingRoomTypes =
                  returnValue.salesHousingRoomTypes;
              if (returnValue.hasOwnProperty("salesHousingConcessions"))
                itineraryData.salesHousingConcessions =
                  returnValue.salesHousingConcessions;
              if (returnValue.hasOwnProperty("lodgingRecords"))
                itineraryData.lodgingRecords = returnValue.lodgingRecords;
              else itineraryData.lodgingRecords = [];
              console.log("itineraryData :: " + itineraryData);
              itineraryData.concessionRecords =
                returnValue.salesHousingConcessions;
              itineraryData.distanceFromEventOptions =
                returnValue.distanceFromEventOptions;
              itineraryData.hotelStars = returnValue.hotelStars;
              itineraryData.hotelTypes = returnValue.hotelTypes;
              itineraryData.preferredBrands = returnValue.preferredBrands;
              itineraryData.roomTypes = returnValue.roomTypes;
              itineraryData.concessionHousingTypes =
                returnValue.concessionHousingTypes;
              itineraryData.concessionCorporateTypes =
                returnValue.concessionCorporateTypes;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getGroundPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForGround"))
                itineraryData.salesForGround = returnValue.salesForGround;
              if (returnValue.hasOwnProperty("groundRecords"))
                itineraryData.groundRecords = returnValue.groundRecords;
              else itineraryData.groundRecords = [];
              itineraryData.tripTypesGround = returnValue.tripTypesGround;
              itineraryData.locationPickUpTypes =
                returnValue.locationPickUpTypes;
              itineraryData.locationDropOffTypes =
                returnValue.locationDropOffTypes;
              itineraryData.vehicleTypesGround = returnValue.vehicleTypesGround;
              itineraryData.groupTypesGround = returnValue.groupTypesGround;
              itineraryData.amenitiesGround = returnValue.amenitiesGround;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getAirPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForAir"))
                itineraryData.salesForGround = returnValue.salesForAir;
              if (returnValue.hasOwnProperty("flightRecords"))
                itineraryData.flightRecords = returnValue.flightRecords;
              else itineraryData.flightRecords = [];
              itineraryData.classServicesAir = returnValue.classServicesAir;
              itineraryData.preferredAirlinesAir =
                returnValue.preferredAirlinesAir;
              component.set("v.itineraryData", itineraryData);
              break;
            case "getFreightPage":
              var itineraryData = component.get("v.itineraryData");
              if (returnValue.hasOwnProperty("salesForFreight"))
                itineraryData.salesForGround = returnValue.salesForFreight;
              if (returnValue.hasOwnProperty("freightRecords"))
                itineraryData.freightRecords = returnValue.freightRecords;
              else itineraryData.freightRecords = [];
              itineraryData.groupTypesFreight = returnValue.groupTypesFreight;
              component.set("v.itineraryData", itineraryData);
              break;
            case "saveProductionServices":
              var firstService = returnValue.split(";")[0];
              if (firstService == "Housing")
                component.set("v.menuSelected", "housing");
              if (firstService == "Ground Travel")
                component.set("v.menuSelected", "ground");
              if (firstService == "Air") component.set("v.menuSelected", "air");
              if (firstService == "Freight")
                component.set("v.menuSelected", "freight");
              var itineraryData = component.get("v.itineraryData");
              itineraryData.services = returnValue;
              component.set("v.itineraryData", itineraryData);
              break;
            case "upsertItineraryRecord":
              var callToChild = $A.get("e.c:VoyajerCallToChild");
              if (returnValue.hasOwnProperty("errorMessage")) {
                callToChild.setParams({
                  action: returnValue.errorMessage,
                  data: {}
                });
              } else {
                var data = { record: returnValue.record };
                if (returnValue.hasOwnProperty("salesForHousing"))
                  data.salesForHousing = returnValue.salesForHousing;
                if (returnValue.hasOwnProperty("salesHousingRoomTypes"))
                  data.salesHousingRoomTypes =
                    returnValue.salesHousingRoomTypes;
                if (returnValue.hasOwnProperty("salesHousingConcessions"))
                  data.salesHousingConcessions =
                    returnValue.salesHousingConcessions;
                if (returnValue.hasOwnProperty("salesForGround"))
                  data.salesForGround = returnValue.salesForGround;
                callToChild.setParams({
                  action: returnValue.action,
                  data: data
                });
              }
              callToChild.fire();
              break;
            case "deleteItineraryRecord":
              var callToChild = $A.get("e.c:VoyajerCallToChild");
              if (returnValue.hasOwnProperty("errorMessage")) {
                callToChild.setParams({
                  action: returnValue.errorMessage,
                  data: {}
                });
              } else {
                callToChild.setParams({
                  action: returnValue.action,
                  data: {}
                });
              }
              callToChild.fire();
              break;
            case "subimtProductionItineraries":
              if (returnValue) {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "success",
                  message: "Your itinerary has been submitted."
                });
                toastEvent.fire();
                component.set("v.mainContent", "dashboard");
              } else {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                  type: "error",
                  message:
                    "Something went wrong. Please refresh the page and try again."
                });
                toastEvent.fire();
              }
              break;
            case "updateUserName":
              var client = component.get("v.client");
              client.userInfo = returnValue;
              component.set("v.client", client);
              self.showMessage(
                "success",
                "Done!",
                "Your profile has been updated."
              );
              break;
            case "saveLodgingPreferences":
              var client = component.get("v.client");
              client.preferencesSelected = returnValue;
              component.set("v.client", client);
              self.showMessage(
                "success",
                "Done!",
                "Your Lodging preferences has been updated."
              );
              break;
            case "getOptionsHousing":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              if (returnValue.serviceData.communityNoteAvailable === true) {
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }

              break;
            case "getOptionsHousingPreview":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              component.set("v.officePreference",returnValue.userInfo.Housing_Preference__c);
              console.log('returnValue.userInfo.Housing_Preference__c :: ' + returnValue.userInfo.Housing_Preference__c);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              if (returnValue.serviceData.communityNoteAvailable === true) {
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              break;
            case "getOptionsHousingDetail":
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getOptionsGT":
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getOptionsGTDetail":
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getOptionsAir":
              console.log("inside GT getter");
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              console.log("communityNotes" + component.get("v.communityNotes"));
              console.log(
                "showCommunityNote" + component.get("v.showCommunityNote")
              );
              console.log("attempting to add hide class");
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getOptionsAirPreview":
              console.log("inside GT getter");
              component.set("v.serviceData", returnValue.serviceData);
              component.set("v.bidOptions", returnValue.bidOptions);
              /* need to try and fix a span class marker rich text issue */
              noteFixed = "";
              if (returnValue.serviceData) {
                if (returnValue.serviceData.communityNote) {
                  noteFixed = returnValue.serviceData.communityNote.replace(
                    '<span class="marker">',
                    '<span class="marker" style="background-color:yellow">'
                  );
                }
              }
              component.set("v.communityNotes", noteFixed);
              component.set("v.modalTitle", "A Message From Your Rebel");
              if (returnValue.serviceData.communityNoteAvailable === true) {
                console.log("inside shownote");
                component.set(
                  "v.showCommunityNote",
                  returnValue.serviceData.communityNoteAvailable
                );
              }
              console.log("attempting to add hide class");
              $A.util.addClass(component.find("loadingPage"), "slds-hide");
              break;
            case "getCommunityNote":
              console.log(returnValue);
              let theResponse = returnValue;
              if (theResponse != "") {
                component.set("v.communityNote", returnValue);
                component.set("v.openSelectOptionsAlert", true);
              }
              break;
            case "showMessages":
              component.set("v.openSelectOptionsAlert", true);
            case "submitBidSelected":
              var result = returnValue;
              if (returnValue == "done") {
                self.showMessage(
                  "success",
                  "Done!",
                  "The option has been selected."
                );
                component.set("v.mainContent", "dashboard");
              } else
                self.showMessage(
                  "error",
                  "",
                  "Something went wrong. Please contact Road Rebel Support team."
                );
              break;
            case "getOptionsAirDetail":
              console.log(returnValue.optionDetailRecord);
              component.set(
                "v.optionDetailRecord",
                returnValue.optionDetailRecord
              );
              break;
            case "getVendorBids":
              component.set("v.bids", returnValue);
              break;
            case "getVendorProductionBids":
              component.set("v.productionName", returnValue.productionName);
              component.set(
                "v.productionCompany",
                returnValue.productionCompany
              );
              component.set(
                "v.productionAssocUserName",
                returnValue.productionAssocUserName
              );
              component.set(
                "v.productionAssocUserPhone",
                returnValue.productionAssocUserPhone
              );
              component.set(
                "v.productionAssocUserEmail",
                returnValue.productionAssocUserEmail
              );
              component.set(
                "v.productionAssocRole",
                returnValue.productionAssocRole
              );
              component.set("v.itineraries", returnValue.itineraries);
              break;
            case "getReservationHousingDetail":
              component.set(
                "v.reservationDetail",
                returnValue.reservationDetailRecord
              );
              console.log("getReservationHousingDetail");
              console.log(returnValue.reservationDetailRecord);
              break;
            case "getReservationGTDetail":
              component.set(
                "v.reservationDetail",
                returnValue.reservationDetailRecord
              );
              console.log("getReservationGTDetail");
              console.log(returnValue.reservationDetailRecord);
              break;
            case "getContactUsData":
              component.set("v.contactUsData", returnValue);
              console.log(
                "getContactUsData - returnValue = " +
                  JSON.stringify(returnValue)
              );
              break;
            case "getDocuments":
              component.set("v.lsDocuments", returnValue.lsDocuments);
              component.set("v.lsDocumentsAux", returnValue.lsDocuments);
              break;
            case "saveDocument":
              console.log(returnValue);
              console.log("saveDocument success!");
              // self.showMessage("success","Done!","Your document has been successfully uploaded.");
              // call 'toastEvent' only work on one.app
              break;
            case "getVendorHousingBid":
            case "getVendorGroundBid":
              component.set(
                "v.productionOfficePreference",
                returnValue.productionOfficePreference
              );
              component.set("v.bidData", returnValue);
              break;
            case "unabledVendorBid":
              component.set("v.mainContent", "dashboardBids");
              self.showMessage("success", "", "Thanks for your answer.");
              break;
            default:
              alert(
                "Please add your method to the helper controller to know what to do with the response"
              );
              break;
          }
        } else if (state === "INCOMPLETE") {
          if (errors[0] && errors[0].message) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              title: "Internal Error",
              message: errors[0].message
            });
            toastEvent.fire();
          }
        } else if (state === "ERROR") {
          var errors = response.getError();
          if (errors) {
            if (errors[0] && errors[0].message) {
              var toastEvent = $A.get("e.force:showToast");
              toastEvent.setParams({
                type: "error",
                title: "Internal Error",
                message: errors[0].message
              });
              toastEvent.fire();
            }
          } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              title: "Internal Error",
              message: "Unknown error"
            });
            toastEvent.fire();
          }
        }
        $A.util.addClass(component.find("loadingPage"), "slds-hide");
      })
    );
    $A.enqueueAction(action);
    //$A.util.addClass(component.find("loadingPage"), "slds-hide");
  },
  getCloseOutRevenue: function (component) {
      var data = {};
      data.serviceId = component.get("v.serviceId");
      data.accountId = component.get("v.client").userInfo.Contact.AccountId;
      var action = component.get("c.getCloseOutHousingVAT");
      action.setParams({ data: JSON.stringify(data) });
      action.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                component.set("v.revenueVatData", response.getReturnValue());
                //alert("From server: " + response.getReturnValue());
            } else if (state === "ERROR") {
                var errors = response.getError();
                if (errors) {
                    if (errors[0] && errors[0].message) {
                        console.log("Error message: " + 
                                 errors[0].message);
                    }
                } else {
                    console.log("Unknown error");
                }
            }
        });
        $A.enqueueAction(action);
  },
  updateRevenue: function (component, data) {
      var action = component.get("c.updateVATDetails");
      action.setParams({ data: JSON.stringify(data) });
      action.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                //component.set("v.revenueVatData", response.getReturnValue());
                //alert("From server: " + response.getReturnValue());
            } else if (state === "ERROR") {
                var errors = response.getError();
                if (errors) {
                    if (errors[0] && errors[0].message) {
                        console.log("Error message: " + 
                                 errors[0].message);
                    }
                } else {
                    console.log("Unknown error");
                }
            }
        });
        $A.enqueueAction(action);
  },
  showMessage: function (type, title, message) {
    var toastEvent = $A.get("e.force:showToast");
    toastEvent.setParams({
      type: type,
      title: title,
      message: message
    });
    toastEvent.fire();
  }
});
```
### VoyajerController

```
({
	doInit: function (component, event, helper) {
		//helper.checkCommunityNote(component, event, helper);
		var urlString = window.location.href;
		var baseURL = urlString.substring(0, urlString.indexOf("/s"));
		component.set("v.sitePrefix", baseURL);

		var sPageURL = decodeURIComponent(window.location.search.substring(1)),
			sURLVariables = sPageURL.split("&"),
			sParameterName,
			hco = "",
			service = "",
			optionRecordId = "",
			stayId = "",
			i;
		for (i = 0; i < sURLVariables.length; i++) {
			sParameterName = sURLVariables[i].split("=");
			if (sParameterName[0] === "hco") hco = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "service") service = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "stayId") stayId = sParameterName[1] === undefined ? "" : sParameterName[1];
			if (sParameterName[0] === "record") optionRecordId = sParameterName[1] === undefined ? "" : sParameterName[1];
		}
		component.set("v.hco", hco);
		optionRecordId = optionRecordId.trim();
		if (optionRecordId.length === 18 && !!optionRecordId) {
			switch (service) {
				case "lodging":
					service = "optionsHousing";
					break;
				case "ground":
					service = "optionsGT";
					break;
				case "freight":
					service = "optionsFreight";
					break;
				case "air":
					service = "optionsAir";
					break;
				default:
					service = "";
					optionRecordId = "";
					break;
			}
		} else {
			service = "";
			optionRecordId = "";
		}
		component.set("v.typeOfService", service);
		component.set("v.optionRecordId", optionRecordId);
		helper.crud(component, "getClient", {});
	},

	loadJquery: function (component, event, helper) {
		jQuery(document).ready(function () {});
	},

	loadDashboardContent: function (component, event, helper) {
		component.set("v.productionSelected", "");
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access this dashboard page.",
				});
				toastEvent.fire();
				break;
			case "Customer":
				component.set("v.mainContent", "dashboard");
				break;
			default:
				component.set("v.mainContent", "dashboardBids");
				break;
		}
	},

	loadReportsContent: function (component, event, helper) {
		component.set("v.productionSelected", "");
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access to this page.",
				});
				toastEvent.fire();
				break;
			default:
				component.set("v.mainContent", "reports");
				break;
		}
	},

	loadContactUsContent: function (component, event, helper) {
		component.set("v.mainContent", "contactus");
	},

	loadUserContent: function (component, event, helper) {
		var userProfile = component.get("v.userProfile");
		switch (userProfile) {
			case "Forbidden":
				component.set("v.mainContent", "");
				var toastEvent = $A.get("e.force:showToast");
				toastEvent.setParams({
					type: "error",
					title: "Your are not a community user!",
					message: "Your have no access to this page.",
				});
				toastEvent.fire();
				break;
			case "Customer":
				component.set("v.mainContent", "user");
				$A.util.removeClass(component.find("loadingPage"), "slds-hide");
				break;
			default:
				component.set("v.mainContent", "vendor");
				break;
		}
	},

	logout: function (component, event, helper) {
		component.set("v.mainContent", "logout");
		window.location.replace(component.get("v.sitePrefix") + "/secur/logout.jsp");
	},

	handleCommunicationEvent: function (component, event, helper) {
		var data = {};
		console.log("case: " + event.getParam("action"));
		switch (event.getParam("action")) {
			case "refreshBidsSelected":
				var bidsSelected = event.getParam("data");
				component.set("v.bidsSelected", bidsSelected);
			case "updateVATAddressData":
				data = event.getParam("data");
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "updateVATData", data);
				break;
			case "loadProductions":
				setTimeout($A.getCallback(helper.crud.bind(this, component, "getProductions", data)), 0);
				break;
			case "showMessages":
				component.set("v.openSelectOptionsAlert", true);
				break;
			case "showDashboard":
				component.set("v.mainContent", "dashboard");
				break;
			case "newProduction":
				data.Name = event.getParam("data").productionName;
				data.CloseDate = event.getParam("data").startDate;
				data.ContactId = component.get("v.client").userInfo.ContactId;
				data.AccountId = component.get("v.client").userInfo.Contact.AccountId;
				data.officePreference = component.get("v.officePreference");
				helper.crud(component, "createProduction", data);
				break;
			case "loadItineraries":
				helper.crud(component, "getProductionItineraries", data);
				break;
			case "loadProductionServices":
				helper.crud(component, "getProductionServices", data);
				break;
			case "loadMultipleOptions":
				helper.crud(component, "getMultipleOptions", data);
				break;
			case "loadLodgingPage":
				helper.crud(component, "getLodgingPage", data);
				break;
			case "loadGroundPage":
				helper.crud(component, "getGroundPage", data);
				break;
			case "loadAirPage":
				helper.crud(component, "getAirPage", data);
				break;
			case "loadFreightPage":
				helper.crud(component, "getFreightPage", data);
				break;
			case "saveServices":
				data.productionId = event.getParam("data").productionId;
				data.services = event.getParam("data").services;
				helper.crud(component, "saveProductionServices", data);
				break;
			case "saveItineraryRecord":
				data.productionId = component.get("v.productionSelected");
				data.recordType = event.getParam("data").recordType;
				data.record = JSON.parse(JSON.stringify(event.getParam("data").record));
				data.officePreference = component.get("v.productionOfficePreference");
				helper.crud(component, "upsertItineraryRecord", data);
				break;
			case "removeItineraryRecord":
				data.productionId = component.get("v.productionSelected");
				data.recordType = event.getParam("data").recordType;
				data.recordId = event.getParam("data").recordId;
				helper.crud(component, "deleteItineraryRecord", data);
				break;
			case "submitItineraries":
				helper.crud(component, "subimtProductionItineraries", data);
				break;
			case "contentLoaded":
				$A.util.addClass(component.find("loadingPage"), "slds-hide");
				break;
			case "updatingUser":
				$A.util.removeClass(component.find("loadingPage"), "slds-hide");
				break;
			case "refreshUser":
				helper.crud(component, "updateUserName", data);
				break;
			case "updatePassword":
				console.log(event.getParam("data").currentPassword);
				console.log(event.getParam("data").newPassword);
				console.log(event.getParam("data").confirmPassword);
				break;
			case "savePreferences":
				helper.crud(component, "saveLodgingPreferences", data);
				break;
			case "loadOptionsHousing":
				helper.crud(component, "getOptionsHousing", data);
				break;
			case "loadOptionsHousingPreview":
				helper.crud(component, "getOptionsHousingPreview", data);
				break;
			case "loadOptionsHousingDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsHousingDetail", data);
				break;
			case "loadOptionsGT":
				helper.crud(component, "getOptionsGT", data);
				break;
			case "loadOptionsGTDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsGTDetail", data);
				break;
			case "loadOptionsAir":
				helper.crud(component, "getOptionsAir", data);
				break;
			case "loadOptionsAirPreview":
				helper.crud(component, "getOptionsAirPreview", data);
				break;
			case "loadOptionsAirDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsAirDetail", data);
				break;
			case "loadOptionsAirReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsAirDetail", data);
				break;
			case "loadOptionsHousingReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsHousingDetail", data);
				break;
			case "submitOptionSelected":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.productionId = component.get("v.productionSelected");
				data.contactName = component.get("v.client").userInfo.Contact.Name;
				var productions = component.get("v.productions");
				productions.forEach(production => {
					if (production.recordId == data.productionId) data.productionRecordTypeName = production.recordTypeName;
				});
				helper.crud(component, "submitBidSelected", data);
				break;
			case "changeMultipleOptions":
				/* using prefix of change for events fired on changes that aren't crud */
				/* data should have been sent for the VoyajerOptionsReviewSubmitItem insance that was edited */
				let allData = event.getParam("data");
				var theOptionIndex = allData.optionIndex;
				var theOptionData = allData.optionData;
				var theOptionComment = allData.optionComment;

				console.log('theOptionIndex:: ' + theOptionIndex);

				let currentBidOptions = component.get('v.theSelectedBidOptions');

				if (currentBidOptions.length === 0){
					console.log('current length 0');
					let bidOp = new Object();
					bidOp.record = theOptionData.record;
					bidOp.theOptionData = theOptionData;
					bidOp.theOptionIndex = theOptionIndex;
					bidOp.theOptionComment = theOptionComment;
					currentBidOptions.push(bidOp);  
				} else {
					console.log('current length not 0');
					if (currentBidOptions.hasOwnProperty(theOptionIndex)) {
						console.log('current length checking property exists - it does');

						currentBidOptions.forEach(bid => {
							if (bid.theOptionIndex === theOptionIndex) {
								console.log('theOptionIndex :: ' + theOptionIndex);
								console.log('bid theOptionIndex:: ' + bid.theOptionIndex);
								bid.record = theOptionData.record;
								bid.theOptionData = theOptionData;
								bid.theOptionIndex = theOptionIndex;
								bid.theOptionComment = theOptionComment;
							}
						});	
						console.log('updated comment');
					} else {
							let bidOp = new Object();
							bidOp.record = theOptionData.record;
							bidOp.theOptionData = theOptionData;
							bidOp.theOptionIndex = theOptionIndex;
							bidOp.theOptionComment = theOptionComment;
							currentBidOptions.push(bidOp);  
					}
				}

				/* this should be coming over to the helper as a list of bidoptions. */
				console.log('new currentBidOptions lengthh :: ' + currentBidOptions.length);	
				component.set("v.theSelectedBidOptions", currentBidOptions);
				break;
			case "submitMultipleOptionsSelected":
                //Fix By Clay Dev 20 March, 2021 #177292637
                component.set("v.theSelectedBidOptions", event.getParam("data").submittedBids);
				helper.crud(component, "saveMultipleOptionsSelected", data);
				break;
			case "loadOptionsGTReviewSubmit":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getOptionsGTDetail", data);
				break;
			case "loadOptionsHousingCompare":
				data.compareList = event.getParam("data").compareList;
				break;
			case "loadOptionsGTCompare":
				data.compareList = event.getParam("data").compareList;
				break;
			case "loadVendorBids":
				setTimeout($A.getCallback(helper.crud.bind(this, component, "getVendorBids", data)), 0);
				break;
			case "loadVendorProductionBids":
				helper.crud(component, "getVendorProductionBids", data);
				break;
			case "loadReservationHousingDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getReservationHousingDetail", data);
				break;
			case "loadReservationGTDetail":
				data.detailRecordId = event.getParam("data").detailRecordId;
				helper.crud(component, "getReservationGTDetail", data);
				break;
			case "loadContactUsData":
				//data.productionId = event.getParam("data").productionId;
				data.productionId = component.get("v.productionSelected");
				helper.crud(component, "getContactUsData", data);
				break;
			case "loadDocuments":
				data.serviceId = event.getParam("data").serviceId;
				helper.crud(component, "getDocuments", data);
				break;
			case "uploadDocument":
				data.docName = event.getParam("data").docName;
				data.docContentBase64 = event.getParam("data").docContentBase64;
				data.docReName = event.getParam("data").docReName;
				data.docType = event.getParam("data").docType;
				data.docServiceId = event.getParam("data").docServiceId;
				helper.crud(component, "saveDocument", data);
				data.serviceId = event.getParam("data").docServiceId;
				helper.crud(component, "getDocuments", data);
				break;
			case "loadCloseOut":
				data.serviceId = component.get("v.serviceId");
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "getCloseOutHousing", data);
				break;
			case "saveCloseOut":
				helper.crud(component, "upsertCloseOutHousing", JSON.parse(JSON.stringify(event.getParam("data"))));
				break;
			case "loadVendorProfile":
				helper.crud(component, "getVendorProfile", data);
				break;
			case "saveVendorProfile":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorProfile", data);
				break;
			case "loadVendorContacts":
				helper.crud(component, "getVendorContacts", data);
				break;
			case "saveVendorContact":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "upsertVendorContact", data);
				break;
			case "removeContact":
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				data.recordId = event.getParam("data");
				helper.crud(component, "deleteVendorContact", data);
				break;
			case "loadPropertyProfile":
				helper.crud(component, "getPropertyProfile", data);
				break;
			case "savePropertyProfile":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyProfile", data);
				break;
			case "loadPropertyInRoom":
				helper.crud(component, "getPropertyInRoom", data);
				break;
			case "savePropertyInRoom":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyInRoom", data);
				break;
			case "loadPropertyOnSite":
				helper.crud(component, "getPropertyOnSite", data);
				break;
			case "savePropertyOnSite":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updatePropertyOnSite", data);
				break;
			case "loadFleetCoach":
				helper.crud(component, "getFleetCoach", data);
				break;
			case "saveVendorVehicle":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				helper.crud(component, "upsertVendorVehicle", data);
				break;
			case "removeVehicle":
				data.accountId = component.get("v.client").userInfo.Contact.AccountId;
				data.recordId = event.getParam("data");
				helper.crud(component, "deleteVendorVehicle", data);
				break;
			case "saveFleetCoach":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetCoach", data);
				break;
			case "loadFleetChauffeured":
				helper.crud(component, "getFleetChauffeured", data);
				break;
			case "saveFleetChauffeured":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetChauffeured", data);
				break;
			case "loadFleetRental":
				helper.crud(component, "getFleetRental", data);
				break;
			case "saveFleetRental":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateFleetRental", data);
				break;
			case "loadPayment":
				helper.crud(component, "getVendorPayment", data);
				break;
			case "saveVendorPayment":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorPayment", data);
				break;
			case "loadVendorHousingBid":
				helper.crud(component, "getVendorHousingBid", data);
				break;
			case "placeHousingBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorHousingBid", data);
				break;
			case "placeGroundBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "updateVendorGroundBid", data);
				break;
			case "loadVendorGroundBid":
				helper.crud(component, "getVendorGroundBid", data);
				break;
			case "unableToBid":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				helper.crud(component, "unabledVendorBid", data);
				break;
			case "testCommunication":
				data = JSON.parse(JSON.stringify(event.getParam("data")));
				console.log(data);
				break;
			default:
				//alert("Please add your call to the controller");
				break;
		}
	},
});
```

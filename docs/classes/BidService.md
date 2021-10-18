---
layout: default
title: BidService
parent: classes
---

```/**
 * @description       : general Bid actions like multi contract splits are confined to this class
 * @author            : sfdc cb
 * @group             : bids
 * @last modified on  : 09-07-2021
 * @last modified by  : sfdc cb
 **/
public without sharing class BidService {
  /**
   * changeBidWrapperToBidSobject takes Options that were selected for Events (multiple options selected) like VoyajerOptionsEventsSubmit
   * @param  theBidsWrapper the wrapper class data from the Voyajer site for selecting options
   * @return               returns a list of Bid Sobjects to be used in other methods
   */
  public static List<Bid__c> changeBidWrapperToBidSobject(
    List<Object> theBidsWrapper
  ) {
    List<Object> bidOptions = (List<Object>) JSON.deserializeUntyped(
      JSON.Serialize(theBidsWrapper)
    );
    system.debug('bidOptions Size :: ' + bidOptions);
    List<Object> bidOptionsData = new List<Object>();
    List<Bid__c> theBids = new List<Bid__c>();
    Map<Id, Bid__c> bidMap = new Map<Id, Bid__c>();

    for (Object key : bidOptions) {
      Map<String, Object> data = (Map<String, Object>) key;
      String theKey = String.valueOf(key);
      Object theBidOption = data.get('theOptionData');

      system.debug('fld ::: ' + theKey);
      system.debug('data ::: ' + data.keySet());
      system.debug('theOptionData :: ' + data.get('theOptionData'));
      system.debug('theOptionComment :: ' + data.get('theOptionComment'));
      system.debug('optionComments :: ' + data.get('optionComments'));
      system.debug('record :: ' + data.get('record'));
      system.debug('theOptionIndex :: ' + data.get('theOptionIndex'));

      String theBidComment = (String) data.get('optionComments');
      String theBidJSONRecord = data == null ||
        data.get('record') == null
        ? ''
        : JSON.serialize(data.get('record'));
      Bid__c newBid = data == null ||
        data.get('record') == null
        ? new Bid__c()
        : (Bid__c) JSON.deserialize(theBidJSONRecord, Bid__c.class);
      newBid.Selected_option_comments__c = theBidComment;
      system.debug('theBidJSONRecord :: ' + theBidJSONRecord);
      system.debug('newBid :: ' + newBid);

      bidMap.put(newBid.Id, newBid);
    }

    update bidMap.values(); // hopefully gets comments and vendor status written
    return bidMap.values();
  }

  /**
   * contractMultipleBidsCreateStays takes a list of bids and will contract them, creating a new stay where necessary due to an existing contracted bid
   * @param  theBids  takes a list of bid Sobjects and creates multieple stays
   */
  public static void contractMultipleBidsCreateStays(List<Bid__c> theBids) {
    /** Fix By Clay Dev 18 March, 2021 #177292637
		List<String> contractedStatuses = new List<String>{'Contracted','In Contracting','Pending Client Signature'};
		Integer countContracted = [SELECT COUNT() FROM Bid__c WHERE Housing__r.Status__c IN :contractedStatuses];
		**/
    system.debug('theBids ::: ' + theBids);
    /*
        // - get ContractID# from custom settings
        // - update the Bid to In Contracting
        // - if housinghavecontracted do:
          // - query housing data based on bid (roomtypes)
		*/
    system.debug('inside the contract creation method');
    system.debug('inside the contract creation method');
    Set<Id> bidIds = new Set<Id>();
    Dashboard__c cs = Dashboard__c.getOrgDefaults();
    String contractidnumber = DashboardController.getNumberFormat(
      Integer.valueOf(cs.Contract_ID__c)
    );

    for (Bid__c theBid : theBids) {
      bidIds.add(theBid.Id);
    }
    system.debug('bidIds :: ' + bidIds);
    List<Bid__c> bidDataHousing = Test.isRunningTest()
      ? theBids
      : [
          SELECT Id, Housing__c
          //Service_Type__c
          FROM Bid__c
          WHERE Id IN :bidIds
        ];
    system.debug('bidDataHousing :: ' + bidDataHousing);
    Map<Id, Id> bidToHousingMap = new Map<Id, Id>();
    for (Bid__c b : bidDataHousing) {
      bidToHousingMap.put(b.Id, b.Housing__c);
    }
    system.debug('bidToHousingMap :: ' + bidToHousingMap);

    Set<Id> housingIds = new Set<Id>();
    for (Bid__c b : theBids) {
      b.Housing__c = bidToHousingMap.get(b.Id);
      housingIds.add(b.Housing__c);
    }

    system.debug('bidToHousingMap :: ' + bidToHousingMap);
    system.debug('housingIds :: ' + housingIds);

    //used to get the housing data so we aren't querying for it in a loop
    Map<Id, Housing__c> housingDataMap = new Map<Id, Housing__c>(
      [
        SELECT
          Id,
          RecordTypeId,
          Date_In__c,
          Date_Out__c,
          City__c,
          Description__c,
          Housing_Preference__c,
          Status_CC__c,
          Trace_Date__c,
          Deadline_Date__c,
          Options_Sent_to_Client__c,
          Tournament__c,
          Other_Venue__c,
          Group__c,
          Venue__c,
          Venue_City__c,
          Status__c,
          Vendor__c,
          Production__c,
          Production_CC__c,
          //Fix By Clay Dev 18 March, 2021 #177292637
          (
            SELECT
              Id,
              Production__c,
              Status__c,
              Start_Date__c,
              End_Date__c,
              Housing__c,
              City__c
            FROM Itinerary__r
          )
        //Service_Type__c
        FROM Housing__c
        WHERE Id = :housingIds
      ]
    );

    system.debug('housingDataMap :: ' + housingDataMap);
    /**Fix By Clay Dev 18 March, 2021 #177292637
		Map<Id, Itinerary__c> itineraryMap = new Map<Id, Itinerary__c>(
			[
				SELECT Id, Production__c, Status__c, Start_Date__c, End_Date__c, Housing__c, City__c
				FROM Itinerary__c
				WHERE Housing__c IN :housingIds
			]
		);

		system.debug ('here are my itineraryMap values :: ' + itineraryMap);


		String productionId = '';
		for (Itinerary__c itin : itineraryMap.values()) {
			system.debug ('here are my itin values :: ' + itin);
			productionId = itin.Production__c;
			itineraryMap.put(itin.Housing__c, itin);
		}**/
    String productionId = '';
    for (Housing__c housing : housingDataMap.values()) {
      if (housing.Itinerary__r.size() > 0) {
        productionId = housing.Itinerary__r[0].Production__c;
        break;
      }
    }

    system.debug(productionId);

    List<Itinerary__c> insertItineraries = new List<Itinerary__c>();
    List<Housing__c> updateHousings = new List<Housing__c>();

    //Fix By Clay Dev 24 April, 2021 #177892080
    String itineraryRecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Itinerary')
      .getRecordTypeId();

    //Fix By Clay Dev 18 March, 2021 #177292637
    Decimal contractId = cs.Contract_ID__c;
    for (Bid__c theBid : theBids) {
      theBid.Contract_ID__c = contractidnumber;
      theBid.Status_Previous__c = theBid.Status__c;
      theBid.Status__c = 'Decision'; //Fix By Clay 3 April, 2021 #177505640 - 'In Contracting';
      theBid.Final_Status__c = 'Decision';
      theBid.Contracted_date_time__c = system.now();

      /**Fix By Clay Dev 18 March, 2021 #177292637
			cs.Contract_ID__c = cs.Contract_ID__c + 1;
			update cs;**/
      contractId = contractId + 1;

      Housing__c newHsng = new Housing__c();
      Housing__c theHousing = housingDataMap.get(theBid.Housing__c);
      newHsng = theHousing.clone();
      newHsng.Vendor__c = housingDataMap.get(theBid.Housing__c).Vendor__c;
      //newHsng.Status_Previous__c = bidDataMap.get(housingBidNumber).b.Housing__r.Status_CC__c;
      newHsng.Status_CC__c = 'Decision'; //'In Contracting';
      newHsng.Trace_Date__c = theHousing != null &&
        theHousing.Trace_Date__c != null
        ? system.today()
        : null;
      newHsng.Original_Stay__c = theHousing.Id;
      newHsng.Production_CC__c = productionId;
      newHsng.Production__c = productionId;
      newHsng.Vendor_lookup__c = theBid.Vendor__c;
      newHsng.Venue__c = housingDataMap.get(theBid.Housing__c).Venue__c;
      newHsng.Venue_City__c = housingDataMap.get(theBid.Housing__c)
        .Venue_City__c;
      newHsng.Tournament__c = housingDataMap.get(theBid.Housing__c)
        .Tournament__c;
      system.debug(newHsng);
      insert newHsng;

      cloneInformationToHousing(theBid, newHsng);

      thebid.Housing__c = newHsng.Id;
      //Fix By Clay Dev 18 March, 2021 #177292637
      thebid.Production__c = productionId;

      //Fix By Clay Dev 18 March, 2021 #177292637
      //Itinerary__c newItinerary = itineraryMap.get([SELECT Id FROM Itinerary__c WHERE Housing__c = :theHousing.Id].Id);
      Itinerary__c newItinerary = theHousing.Itinerary__r[0];
      Itinerary__c itinCloned = newItinerary == null
        ? new Itinerary__c()
        : newItinerary.clone();
      //Fix By Clay Dev 24 April, 2021 #177892080
      itinCloned.RecordTypeId = itineraryRecordTypeId;
      itinCloned.Status__c = 'In Contracting';
      itinCloned.Production__c = productionId;
      itinCloned.Housing__c = newHsng.Id;
      insertItineraries.add(itinCloned);
    }
    //Fix By Clay Dev 18 March, 2021 #177292637
    cs.Contract_ID__c = contractId;
    update cs;
    //Fix By Clay Dev 18 March, 2021 #177292637
    //try {
    if (insertItineraries.size() > 0) {
      insert insertItineraries;
    }

    /** Fix By Clay Dev 18 March, 2021 #177292637
			Map<Id, Housing__c> housingMap = new Map<Id, Housing__c>();
			for (Housing__c housing : updateHousings){
				housingMap.put(housing.Id,housing);
			}
			update housingMap.values();
			for(Bid__c bid : theBids) {
				bid.Production__c = productionId;
			}**/
    //Fix By Clay Dev 18 March, 2021 #177292637
    if (theBids.size() > 0) {
      upsert theBids;
    }
    //Fix By Clay Dev 18 March, 2021 #177292637

    /*} catch (Exception e){
			system.debug (e.getMessage() + ' : ' + e.getStackTraceString());
		}*/
  }

  /**
   * createJournalMultiContract takes a list of bids from the multi contracting process and creates Journals with the information.
   * @param  bidIds bidIds bids you would expect to be in the journals, only a set and it will query for its data.
   */
  public static void createJournalMultiContract(Set<Id> bidIds) {
    Map<Id, Bid__c> theBidAugmentMap = new Map<Id, Bid__c>(
      [
        SELECT
          Housing__c,
          Housing__r.Name,
          Vendor__c,
          Vendor_Contact__c,
          Vendor_Contact__r.Name,
          Vendor__r.Name,
          Selected_option_comments__c
        FROM Bid__c
        WHERE Id IN :bidIds
      ]
    );

    //String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId();
    String journalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
      .get('Trip_Journal')
      .getRecordTypeId();
    String contactName = '';
    String bidVendorName = '';
    String serviceName = '';
    String comments = '';
    String serviceType = '';
    List<JournalCreation.JournalEntry> entries = new List<JournalCreation.JournalEntry>();

    for (Bid__c theBidAugment : theBidAugmentMap.values()) {
      contactName = theBidAugment.Vendor_Contact__r.Name;
      bidVendorName = theBidAugment.Vendor__r.Name;
      serviceName = theBidAugment.Housing__r.Name;
      comments = theBidAugment.Selected_option_comments__c;
      serviceType = 'housing';
      /** #177467960
      entries.add(
        new JournalCreation.JournalEntry(
          'bid',
          theBidAugment.Id,
          bidJournalRT,
          'Selected ' +
          bidVendorName +
          ' for ' +
          (serviceType.equals('housing') ? 'Stay ' : 'Trip ') +
          serviceName +
          ' with the following comments: ' +
          comments
			));**/
      entries.add(
        new JournalCreation.JournalEntry(
          'housing',
          theBidAugment.Housing__c,
          journalRT,
          'Selected ' +
          bidVendorName +
          ' for ' +
          (serviceType.equals('housing') ? 'Stay ' : 'Trip ') +
          serviceName +
          ' with the following comments: ' +
          comments
        )
      );
    }

    if (entries.size() > 0)
      JournalCreation.insertJournal(entries);
  }

  /**
   * cloneInformationToHousing copies the information from a stay to a new stay so that only one stay is contracting a bid
   * @param  dataBid dataBid the bid that is being moved to another stay
   * @param  hData   hData the newly duplicated stay that will have information pulled onto it
   */
  public static void cloneInformationToHousing(
    Bid__c dataBid,
    Housing__c hData
  ) {
    List<Housing__c> roomtypesInsert = new List<Housing__c>();
    Housing__c hDataNew;
    for (Housing__c roomtype : [
      SELECT
        Id,
        Units__c,
        Unit_Type__c,
        Special_Notes__c,
        Date_In__c,
        Date_Out__c,
        Rate__c,
        Nights_CC__c,
        Sales_Housing__c,
        Room_Type__c,
        Projected_Units__c,
        Projected_Room_nights__c
      FROM Housing__c
      WHERE
        RecordType.DeveloperName = 'Room_Types_Ops'
        AND Production_CC__c = :dataBid.Production__c
        AND Sales_Housing__c = :dataBid.Housing__c
        AND Bid__c = NULL
      ORDER BY CreatedDate DESC
    ]) {
      hDataNew = roomtype.clone();
      hDataNew.Id = null;
      hDataNew.Production_CC__c = dataBid.Production__c;
      hDataNew.Sales_Housing__c = hData.Id;
      hDataNew.RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Room_Types_Ops')
        .getRecordTypeId();
      roomtypesInsert.add(hDataNew);
    }

    List<Concessions__c> concessionsInsert = new List<Concessions__c>();
    Concessions__c cDataNew;
    for (Concessions__c concession : [
      SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c
      FROM Concessions__c
      WHERE
        Production__c = :dataBid.Production__c
        AND Housing__c = :dataBid.Housing__c
      ORDER BY CreatedDate DESC
    ]) {
      cDataNew = concession.clone();
      cDataNew.Id = null;
      cDataNew.Production__c = dataBid.Production__c;
      cDataNew.Housing__c = hData.Id;
      concessionsInsert.add(cDataNew);
    }

    if (roomtypesInsert.size() > 0)
      insert roomtypesInsert;
    if (concessionsInsert.size() > 0)
      insert concessionsInsert;
  }

  /**
   * submitInitialBidOnMultiContact used to handle the initial submission of a bid in a multi bid contracting situation.  should flow into te
   * @param  theBids theBids a list of bids that should be treated independently but bulkified for future
   * @return         return returns success if it should continue the process
   */
  @AuraEnabled
  public static Boolean submitInitialBidOnMultiContact(List<Bid__c> theBids) {
    Bid__c theBid; /* used at the bottom for error handling */
    Boolean success = true;
    try {
      theBid = theBids[0];
      String productionId = theBid.Production__c;

      update new Bid__c(
        Id = theBid.Id,
        Status__c = 'Decision', //'In Contracting',
        Final_Status__c = 'Decision', //'In Contracting',
        Selected_option_comments__c = theBid.Selected_option_comments__c
      );
      theBid.Status__c = theBid.Final_Status__c = 'Decision';
      //Fix By Clay Dev 18 March, 2021 #177292637
      List<Housing__c> searchHousing = [
        SELECT Id, Status_CC__c, Trace_Date__c, (SELECT Id FROM Itinerary__r)
        FROM Housing__c
        WHERE Id = :theBid.Housing__c
        LIMIT 1
      ];
      String bidVendorId = theBid.Vendor__c == null ? '' : theBid.Vendor__c; // change by clay to update the bid options info with the vendor on the first bid work it doe
      if (!searchHousing.isEmpty()) {
        update new Housing__c(
          Id = searchHousing.get(0).Id,
          Status_CC__c = 'Decision', //'In Contracting',
          Vendor_lookup__c = (String.isNotBlank(bidVendorId)
            ? bidVendorId
            : null),
          Status_Previous__c = searchHousing.get(0).Status_CC__c,
          Trace_Date__c = searchHousing[0].Trace_Date__c != null
            ? system.today()
            : null
        );
        //Fix By Clay Dev 18 March, 2021 #177292637
        update new Itinerary__c(
          Id = searchHousing[0].Itinerary__r[0].Id,
          Status__c = 'In Contracting'
        );
      }

      Map<String, Id> coordinators = new Map<String, Id>();
      for (Production_Associations__c pa : [
        SELECT User__c, Team_Roles__c
        FROM Production_Associations__c
        WHERE Production_Opp__c = :productionId AND Team_Roles__c != NULL
      ]) {
        if (pa.Team_Roles__c.contains('Primary Housing Coordinator'))
          coordinators.put('housingCoordinator', pa.User__c);
        if (pa.Team_Roles__c.contains('Primary GT Coordinator'))
          coordinators.put('groundCoordinator', pa.User__c);
        if (pa.Team_Roles__c.contains('Primary Air Coordinator'))
          coordinators.put('airCoordinator', pa.User__c);
        if (pa.Team_Roles__c.contains('Primary Freight Coordinator'))
          coordinators.put('freightCoordinator', pa.User__c);
      }
      List<Bid__c> backendContractCoordinator = [
        SELECT
          Contracting_Back_End_Coordinator__c,
          Contracting_Back_End_Coordinator__r.Email,
          Vendor_Contact__r.Name,
          Vendor__r.Name,
          Selected_option_comments__c,
          Housing__r.Name
        FROM Bid__c
        WHERE Id = :theBid.Id AND Contracting_Back_End_Coordinator__c != NULL
        LIMIT 1
      ];
      String userAssigned = '';
      if (!backendContractCoordinator.isEmpty())
        userAssigned = backendContractCoordinator.get(0)
          .Contracting_Back_End_Coordinator__c;
      else {
        userAssigned = coordinators.get('housingCoordinator');
      }
      if (!backendContractCoordinator.isEmpty())
        theBid.Id = backendContractCoordinator.get(0).Id;
      if (!String.isNotBlank(userAssigned)) {
        //insert new Task(
        //	WhatId = theBid.Housing__c,
        //	Subject = 'Client Chose Option',
        //	ActivityDate = Date.today(),
        //	Status = 'Open'
        //OwnerId = userAssigned == null ? UserInfo.getUserId() : userAssigned
        //);
      }
    } catch (Exception e) {
      success = false;
      sendErrorEmail(
        theBid,
        e,
        'Multi Contract Original Stay Update: submitInitialBidOnMultiContact'
      );
    }

    return success;
  }
  @future
  public static void submitMultipleBidsFuture(String theBidJSON) {
  }

  /**
   * handleSubmitMultipleBids called from VoyajerController class to handle submission of bids from the Options screen in community
   * @param  bidData bidData a generic list of objects that should be "bidOptions" that will be turned into bids
   */
  public static void handleSubmitMultipleBids(List<Object> bidData) {
    String theBidJSON = JSON.serialize(bidData);
    List<Bid__c> workableBids = new List<Bid__c>();

    if (bidData != null) {
      //Fix By Clay Dev 18 March, 2021 #177292637
      ApexUtil.BidTrigger_Is_Enabled = false;
      //Turning Off trigger here considering bids will be updates in next piece of code again
      workableBids = changeBidWrapperToBidSobject(bidData);
      //Fix By Clay Dev 18 March, 2021 #177292637
      ApexUtil.BidTrigger_Is_Enabled = true;
    }

    for (Bid__c b : WorkableBids) {
      system.debug(b.Selected_option_comments__c + ' eyyye');
    }
    /* get the stayId */
    Set<Id> housingIds = new Set<Id>();
    for (Bid__c b : workableBids) {
      housingIds.add(b.Housing__c);
    }

    /* check the amount of contracting/contracted things exist already for stay */
    /**Fix By Clay Dev 18 March, 2021 #177292637
		List<String> contractedStatuses = new List<String>{'Contracted','In Contracting','Pending Client Signature'};
		Integer countContracted = [SELECT COUNT() FROM Bid__c WHERE Id IN :housingIds AND (Housing__r.Status__c IN :contractedStatuses OR Housing__r.Status_CC__c IN :contractedStatuses)];
		**/
    Boolean success = true;
    List<Bid__c> bidsToCreateJournal = new List<Bid__c>();

    if (workableBids.size() > 0)
      if (workableBids.size() == 1) {
        /* multi select used and only 1 bid */
        /* this means we just do what it would have done previously */
        //Fix By Clay Dev 18 March, 2021 #177292637
        List<String> contractedStatuses = new List<String>{
          'Contracted',
          'In Contracting',
          'Pending Client Signature'
        };
        Integer countContracted = [
          SELECT COUNT()
          FROM Bid__c
          WHERE
            Id IN :housingIds
            AND (Housing__r.Status__c IN :contractedStatuses
            OR Housing__r.Status_CC__c IN :contractedStatuses)
        ];
        if (countContracted == 0) {
          /* submit the bid */
          try {
            success = submitInitialBidOnMultiContact(workableBids);
            bidsToCreateJournal = workableBids;
          } catch (Exception e) {
            system.debug(
              'I broke submit initial bids :: ' +
              e.getMessage() +
              ' :: ' +
              e.getStackTraceString()
            );
          }
        }
      } else if (workableBids.size() > 1) {
        system.debug('::::: inside wb greater than 1' + workableBids);
        Bid__c initialBid = workableBids[0];
        workableBids.remove(0);
        try {
          success = submitInitialBidOnMultiContact(
            new List<Bid__c>{ initialBid }
          );
          system.debug('success ::::: ' + success);
          if (success == true) {
            contractMultipleBidsCreateStays(workableBids);
          }
        } catch (Exception e) {
          system.debug(
            'I broke during muli workable bids :: ' +
            e.getMessage() +
            ' :: ' +
            e.getStackTraceString()
          );
        }
        system.debug('method exit saveMultipleOptionsSelected');
        bidsToCreateJournal.add(initialBid);
        bidsToCreateJournal.addAll(workableBids);
      }
    createJournalMultiContract(
      new Map<Id, Bid__c>(bidsToCreateJournal).keySet()
    );
  }

  /**
   * sendErrorEmail sends an email to a helpdesk when there is an issue.
   * @param  bid      bid description
   * @param  e        e description
   * @param  workflow workflow description
   */
  static void sendErrorEmail(Bid__c bid, Exception e, String workflow) {
    Messaging.SingleEmailMessage message = new Messaging.SingleEmailMessage();
    message.setToAddresses(new List<String>{ 'claytonboss@gmail.com' });
    message.setSubject('Error occured: ' + e.getMessage());
    //message.setOrgWideEmailAddressId([SELECT Id FROM OrgWideEmailAddress WHERE Address = 'sender@email.com' LIMIT 1].Id);
    //message.setTemplateID([SELECT Id FROM EmailTemplate WHERE DeveloperName ='template_developer_name' LIMIT 1].Id);
    message.setPlainTextBody(
      'An error occured in the process: ' +
      workflow +
      '


Error Message: ' +
      e.getMessage() +
      '


Description: ' +
      e.getStackTraceString()
    );
    message.setWhatId(bid.id);
    message.setSaveAsActivity(false);
    Messaging.SingleEmailMessage[] messages = new List<Messaging.SingleEmailMessage>{
      message
    };
    Messaging.SendEmailResult[] results = Messaging.sendEmail(messages);
    if (results[0].success) {
      System.debug('The email was sent successfully.');
    } else {
      System.debug('The email failed to send: ' + results[0].errors[0].message);
    }
  }
}```

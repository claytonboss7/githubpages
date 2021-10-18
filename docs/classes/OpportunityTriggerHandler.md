---
layout: default
title: OpportunityTriggerHandler
parent: classes
---

```public class OpportunityTriggerHandler {

  public static Boolean hasProcessed = false;
  public static Map<Id, RecordType> oppRecordTypeIdToName = new Map<Id, RecordType>(
          [
            SELECT Id, RecordType.Name, RecordType.DeveloperName
            FROM RecordType
            WHERE SobjectType = 'Opportunity'
          ]);

  //--------------------Handler Methods----------------------
  public static void populateFields(
    Map<Id, Opportunity> oldOpportunityMap,
    List<Opportunity> opportunities
  ) {
    for (Opportunity opportunity : opportunities) {
      if (oldOpportunityMap == null) {
        if (String.isEmpty(opportunity.Office_Location__c))
          opportunity.Office_Location__c = 'RRU';
      } else {
      }
    }
  }

  public static void createDefaultConcessions(
    Map<Id, Opportunity> oldOpportunityMap,
    List<Opportunity> opportunities
  ) {
    system.debug('inside createDefaultConcessions');
    /* based on the market type of the opportunity we will do specific concessions linked to the Production */

    /*- Events
               - Tournament, Weddings, Convention, Conference

          - Live Performance
               - Family Entertainment, Fine Arts, Music, Theater

          - Sports Teams
               - Collegiate , Youth, Profeessional

          - TV/Film 
               - TV, Commercials, Movie
		*/
    List<Concessions__c> concessionsToInsert = new List<Concessions__c>();

    /* loop through opportunities and figure out if we should populate default concessions */
    system.debug('oppRecordTypeIdToName :: ' + oppRecordTypeIdToName);

    for (Opportunity opportunity : opportunities) {
      system.debug('opportunities :: ' + opportunity);
      String theMarketRecordType = oppRecordTypeIdToName.get(opportunity.RecordTypeId) == null ? '' : oppRecordTypeIdToName.get(opportunity.RecordTypeId).DeveloperName;
      String theMarketSubType = opportunity.Market_Type__c;
      List<String> theDefaultConcessions = new List<String>();
      List<String> theDefaultConcessionsFinal = new List<String>();
      List<Concessions__c> theDefaultConcessionsRecords = new List<Concessions__c>();
      system.debug('theMarketRecordType ' + theMarketRecordType);
      system.debug('theMarketSubType ' + theMarketSubType);
      /* inside the production + market and can compare Record Type and Market Type and create concessions accordingly */
      if (theMarketSubType != null && theMarketRecordType != null)
        switch on theMarketRecordType {
          when 'Sports_Teams' {
            theDefaultConcessions = new List<String>{
              'Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment.',
              'Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.',
              'Complimentary High Speed internet in the rooms.',
              'Check-out at 00:00 for the whole group guaranteed.',
              'Complimentary meeting room on GROUND FLOOR for tech gear.',
              'Suite upgrade for Coach, if available.',
              'Hotel guarantees they are following CDC guidelines and hotel brand cleanliness standards.'
            };
            //break;
          }
          when 'Film' {
            if (theMarketSubType == 'TV') {
              theDefaultConcessions = new List<String>{
                'Complimentary parking. If not complimentary, please indicate discounted parking.',
                'Complimentary High Speed internet in the rooms.',
                'F&B discount',
                'Suite upgrade for Coach, if available.',
                'Hotel guarantees they are following CDC guidelines and hotel brand cleanliness standards.'
              };
            } else if (theMarketSubType == 'Movie') {
              theDefaultConcessions = new List<String>{
                'Complimentary meeting room on GROUND FLOOR for tech gear.',
                'Complimentary parking. If not complimentary, please indicate discounted parking.',
                'Complimentary High Speed internet in the rooms.',
                'F&B discount',
                'Hotel guarantees they are following CDC guidelines and hotel brand cleanliness standards.'
              };
            }
            //break;
          }
          when 'Live_Performance' {
            system.debug('inside live performance');
            theDefaultConcessions = new List<String>{
              'Complimentary High Speed internet in the rooms.',
              'Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.',
              'Comp room request (1 for 20)',
              'Suite upgrade for company manager, if available.',
              'Hotel guarantees they are following CDC guidelines and hotel brand cleanliness standards.'
            };
            //break;
          }
          when 'Collegiate_and_Tournament' {
            if (theMarketSubType == 'Tournament') {
              theDefaultConcessions = new List<String>{
                'Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment.',
                'Complimentary High Speed internet in the rooms.',
                'Complimentary parking. If not complimentary, please indicate discounted parking.',
                'Booking link requested.',
                'Hotel guarantees they are following CDC guidelines and hotel brand cleanliness standards.'
              };
            }
            //break;
          }
        }

      /* pass our strings into the method to create Concession records for each string as Concessions Requested */
      theDefaultConcessionsRecords = createConcessions(
        theDefaultConcessions,
        opportunity.Id
      );
      concessionsToInsert.addAll(theDefaultConcessionsRecords);
      system.debug(
        'theDefaultConcessionsRecords' + theDefaultConcessionsRecords
      );
      system.debug('concessionsToInsert' + concessionsToInsert);
    }

    try {
      system.debug('inserting concessionsToInsert');
      if (concessionsToInsert.size() > 0)
        insert concessionsToInsert;
    } catch (Exception e) {
      //RoadRebelUtils.sendQAEmail(e);
    }
  }

  public static List<Concessions__c> createConcessions(
    List<String> concessions,
    String opportunityId
  ) {
    system.debug('inside our create concessions method');

    List<Concessions__c> concessionsToInsert = new List<Concessions__c>();

    for (String concession : concessions) {
      concessionsToInsert.add(
        new Concessions__c(
          Production__c = opportunityId,
          Concession_Type__c = 'Housing',
          Concessions_Requested__c = concession
        )
      );
    }

    return concessionsToInsert;
  }
}```

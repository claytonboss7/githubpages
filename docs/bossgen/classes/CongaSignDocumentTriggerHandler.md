---
layout: default
title: CongaSignDocumentTriggerHandler
parent: classes
---
# Metadata Type
classes


# Filename 
CongaSignDocumentTriggerHandler


# Raw XML
```
/**
 * @description       : conga documents trigger handler
 * @author            : sfdc cb
 * @group             : triggerhandlerss
 * @last modified on  : 09-07-2021
 * @last modified by  : sfdc cb
 **/
public with sharing class CongaSignDocumentTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;

  public Boolean IsDisabled() {
    return TriggerDisabled;
  }

  public void BeforeInsert(List<SObject> newItems) {
  }
  public void BeforeUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
  }
  public void BeforeDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, APXT_CongaSign__Document__c> newCongaTransactionMap = (Map<Id, APXT_CongaSign__Document__c>) newItems;
    contentDocumentUpdates(newCongaTransactionMap);
  }

  public void AfterUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
  }
  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  public static void contentDocumentUpdates(
    Map<Id, APXT_CongaSign__Document__c> newCongaTransactionMap
  ) {
    Set<String> sentTransactionIdSet = new Set<String>();
    for (
      APXT_CongaSign__Document__c congaSignDoc : newCongaTransactionMap.values()
    ) {
      if (
        congaSignDoc.APXT_CongaSign__Transaction__c != null &&
        congaSignDoc.APXT_CongaSign__Type__c == 'Original'
      ) {
        sentTransactionIdSet.add(congaSignDoc.APXT_CongaSign__Transaction__c);
      }
    }
    Map<String, APXT_CongaSign__Transaction__c> congaTransactionIdToRecMap = new Map<String, APXT_CongaSign__Transaction__c>(
      [
        SELECT Id, Parent_a0D__c
        FROM APXT_CongaSign__Transaction__c
        WHERE Id IN :sentTransactionIdSet
      ]
    );

    Map<Id, ContentDocument> sentCongaDocumentsMap = new Map<Id, ContentDocument>();
    Map<Id, Bid__c> sentBidsMap = new Map<Id, Bid__c>();
    Map<Id, Bid__c> bidsMap = new Map<Id, Bid__c>();

    for (
      APXT_CongaSign__Document__c congaSignDoc : newCongaTransactionMap.values()
    ) {
      if (
        congaSignDoc.APXT_CongaSign__Transaction__c != null &&
        congaTransactionIdToRecMap.containsKey(
          congaSignDoc.APXT_CongaSign__Transaction__c
        )
      ) {
        if (
          congaSignDoc.APXT_CongaSign__Type__c == 'Original' &&
          (String.isNotEmpty(
            !Test.isRunningTest()
              ? congaSignDoc.APXT_CongaSign__ContentDocumentId__c
              : congaSignDoc.APXT_CongaSign__ContentVersionId__c
          ))
        ) {
          sentCongaDocumentsMap.put(
            !Test.isRunningTest()
              ? congaSignDoc.APXT_CongaSign__ContentDocumentId__c
              : congaSignDoc.APXT_CongaSign__ContentVersionId__c,
            new ContentDocument()
          );
          sentBidsMap.put(
            !Test.isRunningTest()
              ? congaSignDoc.APXT_CongaSign__ContentDocumentId__c
              : congaSignDoc.APXT_CongaSign__ContentVersionId__c,
            new Bid__c(
              Id = congaTransactionIdToRecMap.get(
                  congaSignDoc.APXT_CongaSign__Transaction__c
                )
                .Parent_a0D__c
            )
          );
        }
        bidsMap.put(
          congaTransactionIdToRecMap.get(
              congaSignDoc.APXT_CongaSign__Transaction__c
            )
            .Parent_a0D__c,
          new Bid__c()
        );
      }
    }
    if (!sentCongaDocumentsMap.isEmpty()) {
      if (bidsMap.size() > 0) {
        for (Bid__c bid : [
          SELECT
            id,
            Vendor__r.Name,
            Parent_Start_Date__c,
            Parent_End_Date__c,
            Housing__c
          FROM Bid__c
          WHERE id IN :bidsMap.keySet()
        ]) {
          bidsMap.put(bid.id, bid);
        }
      }
      Map<String, Bid__c> bidIdToRecUpdateMap = new Map<String, Bid__c>();
      Map<String, Housing__c> housingIdToRecUpdateMap = new Map<String, Housing__c>();
      Set<Id> housingContractBidIdSet = new Set<Id>();
      for (ContentDocument document : [
        SELECT id, Title
        FROM ContentDocument
        WHERE id IN :sentCongaDocumentsMap.keySet()
      ]) {
        if (!bidIdToRecUpdateMap.containsKey(sentBidsMap.get(document.id).Id)) {
          bidIdToRecUpdateMap.put(
            sentBidsMap.get(document.id).Id,
            new Bid__c(Id = sentBidsMap.get(document.id).Id)
          );
        }
        Bid__c bidRec = bidIdToRecUpdateMap.get(
          sentBidsMap.get(document.id).Id
        );
        if (
          document.Title.containsIgnoreCase('Contract To Client') ||
          document.Title.containsIgnoreCase('ContractToClient')
        ) {
          bidRec.Final_Status__c = 'Pending Client Signature';
          housingIdToRecUpdateMap.put(
            bidsMap.get(sentBidsMap.get(document.id).id).Housing__c,
            new Housing__c(
              Id = bidsMap.get(sentBidsMap.get(document.id).id).Housing__c,
              Status_CC__c = 'Pending Client Signature'
            )
          );
          bidRec.Contract_to_Client_Last_Send_Date__c = Datetime.now();
        }
        if (document.Title.startsWithIgnoreCase('ContractClientSigned'))
          bidRec.Counter_Needed_Last_Send_Date__c = Datetime.now();
        else if (document.Title.containsIgnoreCase('Rate Agreement'))
          bidRec.Rate_Agreement_Last_Send_Date__c = Datetime.now();
        else if (document.Title.containsIgnoreCase('Housing Contract')) {
          bidRec.Housing_Contract_Last_Send_Date__c = Datetime.now();
          housingContractBidIdSet.add(bidRec.Id);
        } else if (document.Title.containsIgnoreCase('Trip Details Update'))
          bidRec.Trip_Details_Update_Last_Send_Date__c = Datetime.now();
        else if (document.Title.containsIgnoreCase('Transportation Contract'))
          bidRec.Transportation_Contract_Last_Send_Date__c = Datetime.now();
        else if (document.Title.containsIgnoreCase('Final Contract'))
          bidRec.Final_Contract_Last_Send_Date__c = Datetime.now();
        else if (document.Title.containsIgnoreCase('PickUp Report'))
          bidRec.Pick_Up_Last_Send_Date__c = Datetime.now();

        document.Title = (document.Title.subStringBefore('.pdf') +
          (String.isNotBlank(
              bidsMap.get(sentBidsMap.get(document.id).id).Vendor__r.Name
            ) &&
            !document.Title.containsIgnoreCase(
              bidsMap.get(sentBidsMap.get(document.id).id).Vendor__r.Name
            )
            ? ' ' + bidsMap.get(sentBidsMap.get(document.id).id).Vendor__r.Name
            : '') +
          (bidsMap.get(sentBidsMap.get(document.id).id).Parent_Start_Date__c !=
            null &&
            !document.Title.containsIgnoreCase(
              Datetime.newInstance(
                  bidsMap.get(sentBidsMap.get(document.id).id)
                    .Parent_Start_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd-MMM-yyyy')
            )
            ? ' ' +
              Datetime.newInstance(
                  bidsMap.get(sentBidsMap.get(document.id).id)
                    .Parent_Start_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd-MMM-yyyy')
            : '') +
          (!document.Title.containsIgnoreCase(' - Sent') ? ' - Sent' : ''))
          .left(255);

        sentCongaDocumentsMap.put(document.id, document);
      }

      try {
        if (!bidIdToRecUpdateMap.isEmpty())
          update bidIdToRecUpdateMap.values();
        if (!housingIdToRecUpdateMap.isEmpty())
          update housingIdToRecUpdateMap.values();
        if (!sentCongaDocumentsMap.isEmpty())
          update sentCongaDocumentsMap.values();
        cancelExistingContractingTransaction(
          housingContractBidIdSet,
          sentTransactionIdSet
        );
      } catch (DmlException e) {
        System.debug(
          'CongaSignDocumentTriggerHandler.contentDocumentUpdates() - DmlException: ' +
          e.getMessage()
        );
      }
    }
  }

  private static void cancelExistingContractingTransaction(
    Set<Id> bidIdSet,
    Set<String> currentCongaTxnIdSet
  ) {
    if (bidIdSet != null) {
      Map<String, String> contentDocIdToSignTransactionIdMap = new Map<String, String>();

      for (APXT_CongaSign__Document__c doc : [
        SELECT
          Id,
          APXT_CongaSign__Transaction__c,
          APXT_CongaSign__ContentDocumentId__c,
          APXT_CongaSign__ContentVersionId__c
        FROM APXT_CongaSign__Document__c
        WHERE
          APXT_CongaSign__Type__c = 'Original'
          AND APXT_CongaSign__Transaction__r.Parent_a0D__c IN :bidIdSet
          AND APXT_CongaSign__Transaction__c NOT IN :currentCongaTxnIdSet
          AND APXT_CongaSign__Transaction__r.APXT_CongaSign__Status__c = 'SENT'
      ]) {
        String contentDocId = (!Test.isRunningTest()
          ? doc.APXT_CongaSign__ContentDocumentId__c
          : doc.APXT_CongaSign__ContentVersionId__c);
        if (String.isNotBlank(contentDocId)) {
          contentDocIdToSignTransactionIdMap.put(
            contentDocId,
            doc.APXT_CongaSign__Transaction__c
          );
        }
      }
      APXT_CongaSign.apxt_cancelTransactionsInvocable.CancelTransactionsRequest req = 
                	new APXT_CongaSign.apxt_cancelTransactionsInvocable.CancelTransactionsRequest();
      req.sendEmails = false;
      req.transactionObjectIds = new List<Id>();      
      for (ContentDocument document : [
        SELECT id, Title
        FROM ContentDocument
        WHERE id IN :contentDocIdToSignTransactionIdMap.keySet()
      ]) {
        if (
          !document.Title.containsIgnoreCase('Contract To Client') &&
          !document.Title.containsIgnoreCase('ContractToClient') &&
          !document.Title.startsWithIgnoreCase('ContractClientSigned') &&
          document.Title.containsIgnoreCase('Housing Contract')
        ) {
          req.transactionObjectIds.add(
              contentDocIdToSignTransactionIdMap.get(
              	document.Id
          	  )
          );
        }
      }
      if(req.transactionObjectIds.size() > 0) {
        List<APXT_CongaSign.apxt_cancelTransactionsInvocable.CancelTransactionsRequest> cancelTransactionsRequestList = 
            new List<APXT_CongaSign.apxt_cancelTransactionsInvocable.CancelTransactionsRequest>();
        cancelTransactionsRequestList.add(req);
      	APXT_CongaSign.apxt_cancelTransactionsInvocable.cancelTransactions(cancelTransactionsRequestList);
      }
    }
  }
}
```


# Last Modified


# Usage

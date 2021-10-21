---
layout: default
title: PDF_BidSubmissionLPControllerTest
parent: classes
---
# Metadata Type
classes


# Filename 
PDF_BidSubmissionLPControllerTest


# Raw XML
```
/**
 * @description       : Generates the bid deetails PDF for the Landing Pages using the Guest User License from Voyajer
 * @author            : clay b
 * @group             :
 * @last modified on  : 07-03-2021
 * @last modified by  : clay b
 * Modifications Log
 * Ver   Date         Author   Modification
 * 1.0   06-27-2021   clay b   Initial Version
 **/
@isTest
public with sharing class PDF_BidSubmissionLPControllerTest {
  @TestSetup
  static void createData() {
    TestDataFactory.createHousingDataHotelHousing();
  }

  /**
   * @description tests that the generation of the PDF results in data attached to the controller that we expect like bidsMap
   * @author clay b | 06-27-2021
   **/
  @isTest
  static void testBidSubmissionPDFPageGeneratePDF() {
    PageReference testPage = Page.PDF_BidSubmissionLP;
    Test.setCurrentPage(testPage);
    testPage.getParameters()
      .put('bidid', [SELECT Id, UUID_For_Landing_Page__c FROM Bid__c LIMIT 1].UUID_for_Landing_Page__c);

    PDF_BidSubmissionLPController pdfBidSubmissionController = new PDF_BidSubmissionLPController();
    system.assertNotEquals(pdfBidSubmissionController.bidsMap.size(), 0);
  }

  /**
   * @description tests that the generation of the PDF results in data attached to the controller that we expect like bidsMap
   * @author clay b | 06-27-2021
   **/
  @isTest
  static void testBidSubmissionPDFPageGeneratePDFActionMethod() {
    PageReference testPage = Page.PDF_BidSubmissionLP;
    Test.setCurrentPage(testPage);
    testPage.getParameters()
      .put('bidid', [SELECT Id, UUID_For_Landing_Page__c FROM Bid__c LIMIT 1].UUID_for_Landing_Page__c);
    Bid__c memorializedBid = [SELECT Memorialization_Data__c FROM Bid__c LIMIT 1];
    system.assertEquals(memorializedBid.Memorialization_Data__c, null);

    PDF_BidSubmissionLPController pdfBidSubmissionController = new PDF_BidSubmissionLPController();
    pdfBidSubmissionController.logInitialBidMemorialization();
    memorializedBid = [SELECT Memorialization_Data__c FROM Bid__c LIMIT 1];

    //system.assertNotEquals(pdfBidSubmissionController.bidsMap.size(), 0);
    //  system.assertNotEquals(memorializedBid.Memorialization_Data__c, null);
  }

  @isTest
  static void testBidSubmissionPDFPageGeneratePDFActionMethodMemorializedDataExists() {

    PDFBidData pdfData = new PDFBidData();
    pdfData.theBidData = [SELECT Id FROM Bid__c];
    update new Bid__c(Id = [SELECT Id FROM Bid__c LIMIT 1].Id, Memorialization_Data__c=JSON.serialize(pdfData));
    PageReference testPage = Page.PDF_BidSubmissionLP;
    Test.setCurrentPage(testPage);
    testPage.getParameters()
      .put('bidid', [SELECT Id, UUID_For_Landing_Page__c FROM Bid__c LIMIT 1].UUID_for_Landing_Page__c);
    Bid__c memorializedBid = [SELECT Memorialization_Data__c FROM Bid__c LIMIT 1];
    system.assertNotEquals(memorializedBid.Memorialization_Data__c, null);
    PDF_BidSubmissionLPController pdfBidSubmissionController = new PDF_BidSubmissionLPController();
    pdfBidSubmissionController.logInitialBidMemorialization();
    system.assertNotEquals(pdfBidSubmissionController.bidsMap.size(), 0);
  }
}
```


# Last Modified


# Usage

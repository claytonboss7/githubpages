---
layout: default
title: PDF_CloseOutReportLPControllerTest
parent: classes
---

```/**
 * @description       : Generates the closeout report for the Landing Pages using the Guest User License from Voyajer
 * @author            : clay b
 * @group             : landing pages
 * @last modified on  : 06-27-2021
 * @last modified by  : clay b
 * Modifications Log
 * Ver   Date         Author   Modification
 * 1.0   06-27-2021   clay b   Initial Version
 **/
@isTest
public with sharing class PDF_CloseOutReportLPControllerTest {
  @TestSetup
  static void createData() {
    TestDataFactory.createHousingDataHotelHousing();
  }

  /**
  * @description tests that the constructor causes the bids data to be attached to the controller meaning it would display
  * @author clay b | 06-27-2021
  **/
  @isTest
  static void testCloseOutPDFPageGeneratePDF() {

    PageReference testPage = Page.PDF_CloseOutReportLP;
    Test.setCurrentPage(testPage);
    testPage.getParameters()
      .put('bidid', [SELECT Id, UUID_For_Landing_Page__c FROM Bid__c LIMIT 1].UUID_for_Landing_Page__c);

    PDF_CloseOutReportLPController pdfCloseOutController = new PDF_CloseOutReportLPController();
    system.assertNotEquals(pdfCloseOutController.bidsMap.size(), 0);
  }
}```

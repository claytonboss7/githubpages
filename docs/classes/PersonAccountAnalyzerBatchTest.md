---
layout: default
title: PersonAccountAnalyzerBatchTest
parent: classes
---

```/**
 * @description       : person account conversion scenarios for our conversion process. detailed in the class PersonAccountAnalyzierBatch
 * @author            : clay b
 * @group             : person accounts
 * @last modified on  : 08-26-2021
 * @last modified by  : sfdc cb
 * Modifications Log
 * Ver   Date         Author   Modification
 * 1.0   05-13-2021   clay b   Initial Version
 * 1.1   07-28-2021   clay b   Update event handling for moving events
 **/
@isTest
private class PersonAccountAnalyzerBatchTest {

  public static String theQuery = 'Phone,MailingStreet,MailingState,MailingCity,MailingPostalCode,MailingCountry,OtherStreet,OtherCountry,OtherCity,OtherState,OtherPostalCode,FirstName,LastName,AssistantName,AssistantPhone,Birthdate,Department,DoNotCall,Email,HasOptedOutOfEmail,HomePhone,LeadSource,OtherAddress,MailingAddress,MobilePhone,OtherPhone,Title,Id,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId,Account.Name FROM Contact WHERE PersonAccountConversion__c = true';

  public static String thePersonAccountRecordTypeId = [
    SELECT Name, SobjectType, IsPersonType, Id
    FROM RecordType
    WHERE SobjectType = 'Account' AND IsPersonType = TRUE
  ]
  .Id;

  /******
   * @testSetup
   * creates the base Business Account + Contact, Tasks attached to Contact
   * any data needed for a specific functional test is creaeted in the method
   */
  @TestSetup
  static void makeData() {
    // BUSINESS ACCOUNTS
    Account testAccount = new Account(
      Name = 'Test Person Acc',
      RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Company').getRecordTypeId()
    );
    insert testAccount;

    // CONTACT THAT WILL BE CONVERTED
    Contact testContact = new Contact(
      LastName = 'Test Person Acc9',
      AccountId = testAccount.Id,
      AssistantName = 'Contact Asst',
      RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName()
        .get('General_Contact')
        .getRecordTypeId()
    );
    insert testContact;

    Account testAccount2 = new Account(
      Name = 'Test Person Acc2',
      RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Company').getRecordTypeId()
    );

    insert testAccount2;

    Task theTask = new Task(Subject = 'Pending Contract', OwnerId = UserInfo.getUserId(), WhoId = testContact.Id);
    Event theEvent = new Event(
      ActivityDateTime = system.now(),
      DurationInMinutes = 1,
      WhoId = testContact.Id,
      subject = 'Test'
    );

    insert theEvent;
    insert theTask;

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Contract To Client',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    ContentDocumentLink cdl = new ContentDocumentLink(
      LinkedEntityId = testContact.Id,
      ContentDocumentId = [SELECT Id FROM ContentDocument LIMIT 1]
      .Id
    );
    insert cdl;

    Production_Associations__c pa = new Production_Associations__c(
      Company__c = testAccount.Id
      //RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Associations__c').getRecordTypeId()
    );

    Contact theContact = new Contact(
      AccountId = testAccount2.Id,
      LastName = 'Clay Boss',
      RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName()
        .get('General_Contact')
        .getRecordTypeId()
    );

    insert theContact;
  }

  /**
   * @description
   * this should test the base conversion of a Business Account + Contact to Person Account
   * scenario:  existing business account with normal contact to convert to person account by updating the PersonAccountConversion__c field
   * asserts:   no person account exists before updating, and one exists afterwards.
   */
  @isTest
  static void PersonAccountAnalyzerBatchTestNormalConversion() {
    Test.startTest();

    String theQuery = 'SELECT Id,Phone,Name,Account.Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account[] theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertEquals(theExistingAccount.size(), 0);

    update new Contact(Id = [SELECT Id FROM Contact LIMIT 1].Id, PersonAccountConversion__c = true);

    Test.stopTest();

    theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];

    system.assertNotEquals(null, theExistingAccount);
    system.debug(theExistingAccount);
  }

  /******
   * @description
   * this should test the base conversion of a Business Account + Contact to Person Account when multiple contacts are in the trigger
   * scenario:  existing business account with normal contact to conver to person account
   * asserts:  no person account exists before updating, and one exists afterwards.
   */
  @isTest
  static void PersonAccountTestMultipleContactsConverted() {
    Test.startTest();

    String theQuery = 'SELECT Id,Name,Phone,Account.Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account[] theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertEquals(theExistingAccount.size(), 0);

    // create another account that will be part of the trigger contacts getting converted
    Account testAccount2 = new Account(
      Name = 'Test Person Acc',
      RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Company').getRecordTypeId()
    );

    insert testAccount2;

    Contact testContact2 = new Contact(
      LastName = 'Test Person Acc22',
      AccountId = testAccount2.Id,
      RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName()
        .get('General_Contact')
        .getRecordTypeId()
    );
    insert testContact2;

    Contact[] contactsToConvert = [SELECT Id, PersonAccountConversion__c FROM Contact WHERE Name != 'Clay Boss'];

    for (Contact c : contactsToConvert) {
      c.PersonAccountConversion__c = true;
    }

    update ContactsToConvert;

    Test.stopTest();

    theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE];
    system.assertEquals(theExistingAccount.size(), 2);
    system.debug(theExistingAccount);
  }

  /******
   * @description
   * this should test the base conversion of a Business Account + Contact to Person Account when multiple contacts are in the trigger (bulk so 100 records)
   * scenario:  existing business account with normal contact to convert to person account
   * asserts:  no person account exists before updating, and 100 new exists afterwards.
   */
  @isTest
  static void PersonAccountTestMultipleContactsConvertedBulk() {
    Test.startTest();

    String theQuery = 'SELECT Id,Name,Account.Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account[] theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertEquals(theExistingAccount.size(), 0);

    // create another account that will be part of the trigger contacts getting converted
    Account[] theAccounts = new List<Account>();
    for (integer x = 0; x < 100; x++) {
      theAccounts.add(
        new Account(
          Name = 'Test Person Acc' + x,
          RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Company').getRecordTypeId()
        )
      );
    }

    insert theAccounts;

    Contact[] theContacts = new List<Contact>();

    for (Account a : theAccounts) {
      theContacts.add(new Contact(accountId = a.Id, LastName = 'Test Contact ' + a.Id));
    }
    insert theContacts;

    Contact[] contactsToConvert = [SELECT Id, PersonAccountConversion__c FROM Contact WHERE Name != 'Clay Boss'];
    for (Contact c : contactsToConvert) {
      c.PersonAccountConversion__c = true;
    }

    update ContactsToConvert;

    Test.stopTest();

    theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE];
    system.assertEquals(theExistingAccount.size(), 101);
    system.debug(theExistingAccount);

    Account[] theExistingAccounts = [
      SELECT
        Id,
        RecordTypeId,
        PersonAssistantName,
        Person_Account_Conversion_Complete__c,
        Person_Account_Conversion_Start__c
      FROM Account
      WHERE Account.isPersonAccount = TRUE
      LIMIT 1
    ];

    system.assertNotEquals(null, theExistingAccounts);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Start__c);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Complete__c);
    system.assertEquals('Contact Asst', theExistingAccounts[0].PersonAssistantName);
  }

  /******
   * @description
   * this should test the existing person account situation where the contact already had a match by name in the system, so we create a new person account to merge with it
   * scenario:  existing person account will be found, and a new person account is created to move all the details and related files to the new place holder person account, which will be merged soon with the existing one
   * asserts:  a new person account was created that didn't exist prior to the job, and it has all of the related files and documents moved to it.
   */
  @isTest
  static void PersonAccountAnalyzerBatchTestPersonAccountExists() {
    Contact theContact = [
      SELECT Id, AccountId
      FROM Contact
      WHERE LastName = 'Test Person Acc9' AND isPersonAccount = FALSE
      LIMIT 1
    ];

    system.debug('-=░©░ starting PersonAccountAnalyzerBatchTestPersonAccountExists');
    // add tasks in for the movement of related lists and tasks
    Task[] theTasks = new List<Task>();
    Event[] theEvents = new List<Event>();
    for (Integer x = 0; x < 10; x++) {
      theTasks.add(new Task(WhoId = theContact.Id, subject = 'Test'));
    }
    for (Integer x = 0; x < 10; x++) {
      theEvents.add(
        (new Event(ActivityDateTime = system.now(), DurationInMinutes = 1, WhoId = theContact.Id, subject = 'Test'))
      );
    }
    insert theTasks;
    insert theEvents;
    Test.startTest();

    String theContactToConvert = '';
    String theAccountofContactToConvert = '';
    String theNewPersonAccount = '';
    String theExistingPersonAccount = '';

    Account testExistingPerson = new Account(
      FirstName = '',
      LastName = 'Test Person Acc9',
      RecordTypeId = thePersonAccountRecordTypeId,
      Phone = '4125551212'
    );
    insert testExistingPerson;

    theContactToConvert = theContact.Id;
    theAccountofContactToConvert = theContact.AccountId;
    theExistingPersonAccount = testExistingPerson.Id;

    // we've isolated our contacts that we can now double check are in their pre configured state before conversion

    // ACR should be for the original Business Account and Contact that are attempting to be converted
    AccountContactRelation[] theACRs = [
      SELECT Id, AccountId, ContactId, Account.Name, Contact.Name
      FROM AccountContactRelation
      WHERE ContactId = :theContact.Id
    ];
    system.assertEquals(theACRs.size(), 1);
    system.assertEquals(theACRs[0].AccountId, theAccountofContactToConvert);
    system.assertEquals(theACRs[0].ContactId, theContactToConvert);
    system.debug('ACRs yo :::: ' + theACRs.size());

    // ContentNote should be attached to the old business account contact
    ContentDocumentLink[] theContent = [
      SELECT Id, LinkedEntityId
      FROM ContentDocumentLink
      WHERE LinkedEntityId = :theContactToConvert
    ];
    system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the Contact
    theTasks = [SELECT Id FROM Task WHERE WhoId = :theContactToConvert];
    system.assertEquals(theTasks.size(), 11);

    /***
     * this is where conversion happens and we will check values after
     */

    String theQuery = 'SELECT Id,MailingStreet,MailingState,MailingCity,MailingPostalCode,OtherStreet,OtherCity,OtherState,OtherPostalCode,Account.Name,FirstName,LastName,Email,Phone,Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertNotEquals(null, theExistingAccount);
    update new Contact(
      Id = [SELECT Id FROM Contact WHERE LastName = 'Test Person Acc9' ORDER BY createddate ASC LIMIT 1]
      .Id,
      PersonAccountConversion__c = true
    );
    Test.stopTest();

    Account[] theAccounts = [
      SELECT Id, RecordTypeId
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :testExistingPerson.Id
      ORDER BY CreatedDate DESC
    ];
    system.debug('sadf ::: ' + theAccounts);

    system.assertEquals(theAccounts.size(), 1);

    // ContentNote should be attached to the old business account contact
    theContent = [SELECT Id, LinkedEntityId FROM ContentDocumentLink WHERE LinkedEntityId = :theAccounts[0].Id];
    //system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the new Person Account not the old contact
    theTasks = [SELECT Id FROM Task WHERE Who.Name = 'Test Person Acc9' AND Who.Type = 'Account'];
    system.assertEquals(theTasks.size(), 0);

    theTasks = [SELECT Id FROM Task WHERE WhoId != :theContactToConvert];
    system.assertEquals(theTasks.size(), 11);

    Event[] theEvents2 = new List<Event>();
    // Tasks should be attached to the new Person Account not the old contact
    theEvents = [SELECT Id FROM Event WHERE Who.Name = 'Test Person Acc9' AND Who.Type = 'Account'];
    system.assertEquals(theEvents.size(), 0);


    theEvents = [SELECT Id FROM Event WHERE WhoId != :theContactToConvert];
    system.assertEquals(theEvents.size(), 11);

    Account[] theExistingAccounts = [
      SELECT Id, RecordTypeId, Person_Account_Conversion_Complete__c, Person_Account_Conversion_Start__c
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :theExistingAccount.Id
      LIMIT 1
    ];

    system.assertNotEquals(null, theExistingAccounts);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Start__c);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Complete__c);

    system.debug('-=░©░ end PersonAccountAnalyzerBatchTestPersonAccountExists');


}

  @isTest
  static void PersonAccountAnalyzerBatchTestTimeStamps() {
    Test.startTest();

    String theQuery = 'SELECT Id,Name,Account.Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account[] theExistingAccount = [
      SELECT Id, RecordTypeId
      FROM Account
      WHERE Person_Account_Conversion_Complete__c != NULL
    ];
    system.assertEquals(theExistingAccount.size(), 0);

    update new Contact(Id = [SELECT Id FROM Contact LIMIT 1].Id, PersonAccountConversion__c = true);

    Test.stopTest();

    theExistingAccount = [
      SELECT Id, RecordTypeId, Person_Account_Conversion_Complete__c, Person_Account_Conversion_Start__c
      FROM Account
      WHERE Account.isPersonAccount = TRUE
      LIMIT 1
    ];

    system.assertNotEquals(null, theExistingAccount);
    system.assertNotEquals(null, theExistingAccount[0].Person_Account_Conversion_Start__c);
    system.assertNotEquals(null, theExistingAccount[0].Person_Account_Conversion_Complete__c);

    system.debug(theExistingAccount);
  }

  /**
  * @description this should test the field value logic we have where it will use the existing contacts field value, if its blank it will use the existing account value, or if they are 2 differnt values for Account and Contact it will flag the record
  * the PersonAssistantName field on the Existing Person Account and The Contact AssistantName field on the contact being converted are different, should be flagged as 'Person Account Needs Attn'
  @author clay b | 05-15-2021
  **/
  @isTest
  static void PersonAccountAnalyzerBatchTestFieldValuesNotNullDifferent() {
    Contact theContact = [SELECT Id, AccountId FROM Contact LIMIT 1];

    system.debug('-=░©░ starting PersonAccountAnalyzerBatchTestPersonAccountExists');
    // add tasks in for the movement of related lists and tasks
    Task[] theTasks = new List<Task>();
    for (Integer x = 0; x < 10; x++) {
      theTasks.add(new Task(WhoId = theContact.Id, subject = 'Test'));
    }
    insert theTasks;
    Test.startTest();

    String theContactToConvert = '';
    String theAccountofContactToConvert = '';
    String theNewPersonAccount = '';
    String theExistingPersonAccount = '';

    Account testExistingPerson = new Account(
      FirstName = '',
      LastName = 'Test Person Acc9',
      RecordTypeId = thePersonAccountRecordTypeId,
      PersonAssistantName = 'Existing Asst'
    );
    insert testExistingPerson;

    theContactToConvert = theContact.Id;
    theAccountofContactToConvert = theContact.AccountId;
    theExistingPersonAccount = testExistingPerson.Id;

    // we've isolated our contacts that we can now double check are in their pre configured state before conversion

    // ACR should be for the original Business Account and Contact that are attempting to be converted
    AccountContactRelation[] theACRs = [
      SELECT Id, AccountId, ContactId, Account.Name, Contact.Name
      FROM AccountContactRelation
      WHERE ContactId = :theContact.Id
    ];
    system.assertEquals(theACRs.size(), 1);
    system.assertEquals(theACRs[0].AccountId, theAccountofContactToConvert);
    system.assertEquals(theACRs[0].ContactId, theContactToConvert);
    system.debug('ACRs yo :::: ' + theACRs.size());

    // ContentNote should be attached to the old business account contact
    ContentDocumentLink[] theContent = [
      SELECT Id, LinkedEntityId
      FROM ContentDocumentLink
      WHERE LinkedEntityId = :theContactToConvert
    ];
    system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the Contact
    theTasks = [SELECT Id FROM Task WHERE WhoId = :theContactToConvert];
    system.assertEquals(theTasks.size(), 11);

    /***
     * this is where conversion happens and we will check values after
     */

    String theQuery = 'SELECT Id,OtherPhone,MailingStreet,MailingState,MailingCity,MailingPostalCode,OtherStreet,OtherCity,OtherState,OtherPostalCode,Account.Name,FirstName,LastName,Email,Phone,Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertNotEquals(null, theExistingAccount);
    update new Contact(
      Id = [SELECT Id FROM Contact WHERE Name != 'Clay Boss' ORDER BY CreatedDate ASC LIMIT 1]
      .Id,
      PersonAccountConversion__c = true
    );
    Test.stopTest();

    Account[] theAccounts = [
      SELECT Id, RecordTypeId
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :testExistingPerson.Id
      ORDER BY CreatedDate DESC
    ];
    system.debug('sadf ::: ' + theAccounts);

    system.assertEquals(theAccounts.size(), 1);

    // ContentNote should be attached to the old business account contact
    theContent = [SELECT Id, LinkedEntityId FROM ContentDocumentLink WHERE LinkedEntityId = :theAccounts[0].Id];
    system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the new Person Account not the old contact
    theTasks = [SELECT Id FROM Task WHERE WhoId = :theContactToConvert];
    system.assertEquals(theTasks.size(), 1);
    theTasks = [SELECT Id FROM Task WHERE WhoId != :theContactToConvert AND Who.Name != 'Clay Boss'];
    //system.assertEquals(theTasks.size(), 11);

    Account[] theExistingAccounts = [
      SELECT
        Id,
        Person_Account_Needs_Attn__c,
        RecordTypeId,
        Person_Account_Conversion_Complete__c,
        Person_Account_Conversion_Start__c
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :theExistingAccount.Id
      LIMIT 1
    ];

    /**
     * Timestamps assertion of the start/end timestamps on our records
     */
    system.assertNotEquals(null, theExistingAccounts);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Start__c);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Complete__c);
    system.assertNotEquals(false, theExistingAccounts[0].Person_Account_Needs_Attn__c);

    system.debug('-=░©░ end PersonAccountAnalyzerBatchTestPersonAccountExists');
  }
  /**
  * @description this should test the field value logic we have where it will use the existing contacts field value, if its blank it will use the existing account value, or if they are 2 differnt values for Account and Contact it will flag the record
  * the PersonAssistantName field on the Existing Person Account and The Contact AssistantName field on the contact being converted are different, should be flagged as 'Person Account Needs Attn'
  @author clay b | 05-15-2021
  **/
  @isTest
  static void PersonAccountAnalyzerBatchTestFieldValuesNotDifferent() {
    Contact theContact = [SELECT Id, AccountId FROM Contact LIMIT 1];

    system.debug('-=░©░ starting PersonAccountAnalyzerBatchTestPersonAccountExists');
    // add tasks in for the movement of related lists and tasks
    Task[] theTasks = new List<Task>();
    for (Integer x = 0; x < 10; x++) {
      theTasks.add(new Task(WhoId = theContact.Id, subject = 'Test'));
    }
    insert theTasks;
    Test.startTest();

    String theContactToConvert = '';
    String theAccountofContactToConvert = '';
    String theNewPersonAccount = '';
    String theExistingPersonAccount = '';

    Account testExistingPerson = new Account(
      FirstName = '',
      LastName = 'Test Person Acc9',
      RecordTypeId = thePersonAccountRecordTypeId
    );
    insert testExistingPerson;

    theContactToConvert = theContact.Id;
    theAccountofContactToConvert = theContact.AccountId;
    theExistingPersonAccount = testExistingPerson.Id;

    // we've isolated our contacts that we can now double check are in their pre configured state before conversion

    // ACR should be for the original Business Account and Contact that are attempting to be converted
    AccountContactRelation[] theACRs = [
      SELECT Id, AccountId, ContactId, Account.Name, Contact.Name
      FROM AccountContactRelation
      WHERE ContactId = :theContact.Id
    ];
    system.assertEquals(theACRs.size(), 1);
    system.assertEquals(theACRs[0].AccountId, theAccountofContactToConvert);
    system.assertEquals(theACRs[0].ContactId, theContactToConvert);
    system.debug('ACRs yo :::: ' + theACRs.size());

    // ContentNote should be attached to the old business account contact
    ContentDocumentLink[] theContent = [
      SELECT Id, LinkedEntityId
      FROM ContentDocumentLink
      WHERE LinkedEntityId = :theContactToConvert
    ];
    system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the Contact
    theTasks = [SELECT Id FROM Task WHERE WhoId = :theContactToConvert];
    system.assertEquals(theTasks.size(), 11);

    /***
     * this is where conversion happens and we will check values after
     */

    String theQuery = 'SELECT Id,OtherPhone,MailingStreet,MailingState,MailingCity,MailingPostalCode,OtherStreet,OtherCity,OtherState,OtherPostalCode,Account.Name,FirstName,LastName,Email,Phone,Name,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId FROM Contact WHERE PersonAccountConversion__c = true';

    Account theExistingAccount = [SELECT Id, RecordTypeId FROM Account WHERE Account.isPersonAccount = TRUE LIMIT 1];
    system.assertNotEquals(null, theExistingAccount);
    update new Contact(
      Id = [SELECT Id, Phone FROM Contact ORDER BY createddate ASC LIMIT 1]
      .Id,
      PersonAccountConversion__c = true
    );
    Test.stopTest();

    Account[] theAccounts = [
      SELECT Id, RecordTypeId
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :testExistingPerson.Id
      ORDER BY CreatedDate DESC
    ];
    system.debug('sadf ::: ' + theAccounts);

    system.assertEquals(theAccounts.size(), 1);

    // ContentNote should be attached to the old business account contact
    theContent = [SELECT Id, LinkedEntityId FROM ContentDocumentLink WHERE LinkedEntityId = :theAccounts[0].Id];
    system.assertEquals(theContent.size(), 1);

    // Tasks should be attached to the new Person Account not the old contact
    theTasks = [SELECT Id, subject, status FROM Task WHERE WhoId = :theContactToConvert];
    system.assertEquals(theTasks.size(), 1);
    theTasks = [SELECT Id FROM Task WHERE Who.Name != 'Clay Boss' AND WhoId != :theContactToConvert];
    //system.assertEquals(theTasks.size(), 11);

    Account[] theExistingAccounts = [
      SELECT
        Id,
        Person_Account_Needs_Attn__c,
        Person_Account_No_Issues__c,
        RecordTypeId,
        Person_Account_Conversion_Complete__c,
        Person_Account_Conversion_Start__c
      FROM Account
      WHERE Account.isPersonAccount = TRUE AND Id != :theExistingAccount.Id
      LIMIT 1
    ];

    /**
     * Timestamps assertion of the start/end timestamps on our records
     */
    system.assertNotEquals(null, theExistingAccounts);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Start__c);
    system.assertNotEquals(null, theExistingAccounts[0].Person_Account_Conversion_Complete__c);
    system.assertEquals(false, theExistingAccounts[0].Person_Account_Needs_Attn__c);
    system.assertEquals(true, theExistingAccounts[0].Person_Account_No_Issues__c);

    system.debug('-=░©░ end PersonAccountAnalyzerBatchTestPersonAccountExists');
  }
}```

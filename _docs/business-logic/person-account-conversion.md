---
title: Person Account Conversion
description: A detailed write up of the custom Person Account Conversion Functionality.
---

# Person Account Converter

_Convert Business Accounts to Person Accounts_
_Last Updated 05162021 by Clay Boss_

## Description

Started as a dataload issue that ended up being scripted to avoid loading 10 files. The package contains a PB and Invokable Apex to do the work of converting person accounts, as well as moving the tasks and notes and files when they exist.

## Usage

![personaccountsusage](https://claytonboss7.github.io/voyajerwiki/assets/img/person-accounts-usage.gif)


On a contact that you wish to convert into a person account, use the "Convert to Person" button on the Contact layout to queue this record up for conversion.  An email will be sent when the conversion is complete with details, assuming the Custom Setting for emails is enabled.  Refer here for information on removing this email.

## Workflow / Logic

- The field "PersonAccountConversion\_\_c" on the Contact object is the Checkbox field that drives the conversion.
- "_Convert to Person_" Action on Contact Object will allow for input of the PersonAccountConversion\_\_c flag
- Process Builder on Contact object catches when "PersonAccountConversion\_\_c" goes to "TRUE"
- Process Builder will pass that Contact into Batch Apex to be processed.
- Business Logic inside of Person Account Converter is as follows:
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/PersonAccountConversion.jpeg)
  - Flow
    - Existing Person Account that matches by Name?
    - Yes 
      - Create Person Account to transfer Business Contact to
      - Copy Fields from existing records to New Person Account and Flag if mismatched fields for same Person (LastName had different value on Existing Person Account and Business Contact being Converted)
      - Move Tasks, ACRs, and ContentDocuments
    - No
      - Go through standard Conversion process
      - Create Account to House Contact 
      - Run validation related to Currency, ReportsTo, Owner, and other criteria
      - Convert RecordTypeId of Account we just created.
  - Email and Logging enabled?
    - Email when complete

### Troubleshooting

- Exception Reports
  - Accounts Flagged for Conversion / Successful Person Accounts Joined Report
    - [https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zJ2kEAE/view]
    - This report will have two side by side reports, the left being the attempted records anthe right being anything that wasn't a Person Account after conversion.

| Field Label | Description |
| --- | --- |
| `Person Account Conversion Start` | Timestamped when the conversion process starts. |
| `Person Account Conversion Complete` | Timestamped when the conversion process ends. |
| `Person Account Conversion No Issues` | If true, all the operations completed without any issues. |
| `Person Account Needs Attn` | If true, the account needs special attention because field values were mismatched. |

<hr width="60%"/>

### Developer Console
  - When running the batch you would see SerialBatchRangeChunkHandler logs popping up for each batch it runs. With this log you will have a comprehensive list of variables and their values while it processed, which could aid in troubleshooting.

### Email and Logging
  - Emails can be enabled to send when the job is finished in the Custom Setting for Road Rebel Settings - Send Person Account Email.

<hr width="30%"/>

## The Execute Anonymous Code Block

```
String theQuery =

   'SELECT MailingStreet,MailingState,MailingCity,MailingPostalCode,OtherStreet,OtherCity,OtherState,OtherPostalCode,FirstName,LastName,AssistantName,AssistantPhone,Birthdate,Department,DoNotCall,Email,HasOptedOutOfEmail,HomePhone,LeadSource,OtherAddress,MailingAddress,MobilePhone,OtherPhone,Title,Id,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId,Account.Name FROM Contact WHERE PersonAccountConversion__c = true ORDER BY LastModifiedDate LIMIT ' + (Test.isRunningTest() ? ids?.size() : 1);

    PersonAccountAnalyzerBatch b = new PersonAccountAnalyzerBatch(theQuery);

    Database.executeBatch(b, 1);
```

## Automated Tests

| Test Name | Description of Test |
| --- | --- |
| `PersonAccountAnalyzerBatchTestPersonAccountExists` | Tests the workflow where Person Account exists, and the new Person Account and field comparison and related record moving is asserted in the class. |
| `PersonAccountAnalyzerBatchTestTimeStamps` | Tests the functionality of the Start and Complete timestamps. |
| `PersonAccountAnalyzerBatchTestFieldValuesNotNullDifferent` | Tests the existing Person Account workflow of copying fields.  Two different values on the same field across the existing records should flag for review. |
| `PersonAccountAnalyzerBatchTestFieldValuesNotDifferent` | Tests the existing Person Account workflow of copying fields.  The same value across the existing records for specific fields should mark as no issues. |

## Field Mappings
The Account and Contact fields, and their associated Person fields, are manually stepped through on the record and compared, and either flagged for review or flagged as having no issues.

** Note: The fields are listed are what would be evaluated for copying the fields for our Person Account Conversion workaround in the existing Person Account side of the workflow. **

The fields on the left side or "key" of the map are Person Account fields and the fields in the right "value" side of the map are from Contact.

```Person Account Field => Contact Field```

```
    Map<String, String> accountFieldContactFieldMap = new Map<String, String>{
      'FirstName' => 'FirstName',
      'LastName' => 'LastName',
      'PersonAssistantName' => 'AssistantName',
      'PersonAssistantPhone' => 'AssistantPhone',
      'PersonBirthDate' => 'BirthDate',
      'PersonDepartment' => 'Department',
      'PersonDoNotCall' => 'DoNotCall',
      'PersonEmail' => 'Email',
      'PersonHasOptedOutOfEmail' => 'HasOptedOutOfEmail',
      'PersonHomePhone' => 'HomePhone',
      'PersonLeadSource' => 'LeadSource',
      'PersonOtherStreet' => 'OtherStreet',
      'PersonOtherCity' => 'OtherCity',
      'PersonOtherState' => 'OtherState',
      'PersonOtherPostalCode' => 'OtherPostalCode',
      'PersonMailingStreet' => 'MailingStreet',
      'PersonMailingCity' => 'MailingCity',
      'PersonMailingPostalCode' => 'MailingPostalCode',
      'PersonMailingState' => 'MailingState',
      'PersonMobilePhone' => 'MobilePhone',
      'PersonOtherPhone' => 'OtherPhone',
      'PersonTitle' => 'Title'
    };
```

## Manifest

- ApexClass: PersonAccountAnalyzerBatch
- ApexClass: PersonAccountAnalyzerBatchTest
- ApexClass: PersonAccountConvertInvoke
- ApexClass: PersonAccountConverterBatch
- Flow: Contact_Convert_person_Account
- QuickAction: Contact - Convert_to_ Person
- CustomField:  PersonAccountConversion\_\_c
- CustomField:  Person_Account_Conversion_Start\_\_c
- CustomField:  Person_Account_Conversion_End\_\_c
- CustomField:  Person_Account_No_Issues\_\_c
- CustomField:  Person_Account_Needs_Attn\_\_c

## Afterthoughts

Some Contacts are causing problems and as of the time of writing this it is not clear why. It will hang up as a batch process and in the UI synchronously it will give a GACK that SF support for whatever reason could not track down.

## Authors

Clay Boss
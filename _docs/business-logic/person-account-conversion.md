---
title: Person Account Conversion
description: A detailed write up of the custom Person Account Conversion Functionality.
---

# Person Account Converter

_Convert Business Accounts to Person Accounts_

## Description

Started as a dataload issue that ended up being scripted to avoid loading 10 files. The package contains a PB and Invokable Apex to do the work of converting person accounts, as well as moving the tasks and notes and files when they exist.

## Usage

On a contact that you wish to convert into a person account, use the "Convert to Person" button on the Contact layout to queue this record up for conversion.  An email will be sent when the conversion is complete with details, assuming the Custom Setting for emails is enabled.  Refer here for information on removing this email.

## Workflow / Logic

The field "PersonAccountConversion\_\_c" on the Contact object is the Checkbox field that drives the conversion.

- "_Convert to Person_" Action on Contact Object will allow for input of the PersonAccountConversion\_\_c flag
- Process Builder on Contact object catches when "PersonAccountConversion\_\_c" goes to "TRUE"
- Process Builder will pass that Contact into Batch Apex to be processed.
- Business Logic inside of Person Account Converter is as follows:
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/PersonAccountConversion.jpeg)
  - Check for existing records
  - **Exists**?
    - 1.0 Create Person Account NEW to move business contact information to
    - 1.1 Move Tasks from Original Contact to new Account from step 1.0
    - 1.2 Move ACRs from Original Contact to new Account from step 1.0
    - 1.3 Move Content Documents to new Account from step 1.0
  - **Didn't Exist**?
    - 2.0 Convert Non Existing Records
    - 2.1 Create Person Account to House Contact Pre-Conversion with
      - Owner
      - Currency
  - 2.2 Attach the Contact we selected for Convert to new Account (The Business Contact we want to convert)
  - 2.3 Run Validation on the Account prior to Conversion
    - Validation will run on new Account created to isolate the business Contact and turn into Person account.
  - 3.0 Converts Contact to Person Account
  - 4.0 Email when complete

### Troubleshooting

- Exception Reports
  - Accounts Flagged for Conversion / Successful Person Accounts Joined Report
    - https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zJ2kEAE/view
    - This report will have two side by side reports, the left being the attempted records anthe right being anything that wasn't a Person Account after conversion.
- Developer Console
  - When running the batch you would see SerialBatchRangeChunkHandler logs popping up for each batch it runs. With this log you will have a comprehensive list of variables and their values while it processed, which could aid in troubleshooting.
- Emails can be enabled to send when the job is finished in the Custom Setting for Road Rebel Settings - Send Person Account Email.

## The Execute Anonymous Code Block

```
String theQuery =

   'SELECT Id,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId,Account.Name
    FROM Contact
    WHERE personaccountconversion__c = true
    AND ispersonaccount=false';

    PersonAccountAnalyzerBatch b = new PersonAccountAnalyzerBatch(theQuery);

    Database.executeBatch(b, 1);
```

## Authors

Clay Boss

## Manifest

- PersonAccountAnalyzerBatch
- PersonAccountAnalyzerBatchTest
- PersonAccountConvertInvoke
- PersonAccountConverterBatch
- Contact_Convert_person_Account.flow-
- Quick Action - Contact - Convert to Person
- Custom Field - PersonAccountConversion\_\_c

## Afterthoughts

Some Contacts are causing problems and as of the time of writing this it is not clear why. It will hang up as a batch process and in the UI synchronously it will give a GACK that SF support for whatever reason could not track down.

- [awesome-readme](https://github.com/matiassingers/awesome-readme)
- [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [dbader](https://github.com/dbader/readme-template)
- [zenorocha](https://gist.github.com/zenorocha/4526327)
- [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)

=== Package Info
Namespace Prefix  Name                      Id                  Alias                     Description              Type
────────────────  ────────────────────────  ──────────────────  ────────────────────────  ───────────────────────  ────────
                  rrPersonAccountConverter  0Ho6g000000k9fFCAQ  rrPersonAccountConverter  RR Person Acc Converter  Unlocked

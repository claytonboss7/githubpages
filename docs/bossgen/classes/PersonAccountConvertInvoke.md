---
layout: default
title: PersonAccountConvertInvoke
parent: classes
---
# Metadata Type
classes


# Filename 
PersonAccountConvertInvoke


# Raw XML
```
/**
 * @description       :
 * @author            : sfdc cb
 * @group             :
 * @last modified on  : 08-26-2021
 * @last modified by  : sfdc cb
**/
public class PersonAccountConvertInvoke {
  @InvocableMethod(
    label='Convert to Person account'
    description='Converts Contacts with the PersonAccountConversion flag set to true to Person Accounts'
    category='Contact'
  )
  public static void convertPersonAccounts(List<ID> ids) {
    // List<Contact> accounts = [SELECT Name FROM Contact WHERE Id IN :ids];
    String theQuery = 'SELECT Phone,MailingStreet,MailingState,MailingCity,MailingPostalCode,MailingCountry,OtherStreet,OtherCity,OtherCountry,OtherState,OtherPostalCode,FirstName,LastName,AssistantName,AssistantPhone,Birthdate,Department,DoNotCall,Email,HasOptedOutOfEmail,HomePhone,LeadSource,OtherAddress,MailingAddress,MobilePhone,OtherPhone,Title,Id,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId,Account.Name FROM Contact WHERE PersonAccountConversion__c = true AND Account.Person_Account_Conversion_Start__c = null ORDER BY LastModifiedDate DESC LIMIT ' + String.valueOf((Test.isRunningTest() ? ids.size() : 1)); //' + ids.size() : '');

    PersonAccountAnalyzerBatch b = new PersonAccountAnalyzerBatch(theQuery);

    Integer batchSize = Test.isRunningTest()
      ? [SELECT COUNT() FROM Contact WHERE PersonAccountConversion__c = TRUE]
      : 1;
    database.executebatch(b, batchSize);
  }
}

/*
finalized query 8/24
String theQuery = 'SELECT Phone,MailingStreet,MailingState,MailingCity,MailingPostalCode,OtherStreet,OtherCity,OtherState,OtherPostalCode,FirstName,LastName,AssistantName,AssistantPhone,Birthdate,Department,DoNotCall,Email,HasOptedOutOfEmail,HomePhone,LeadSource,OtherAddress,MailingAddress,MobilePhone,OtherPhone,Title,Id,ReportsToId,Name,CurrencyISOCode,OwnerId,AccountId,Account.Name FROM Contact WHERE personaccountconversion__c = true and Account.Person_Account_Conversion_Start__c = null AND LastModifiedDate = TODAY LIMIT 1';
PersonAccountAnalyzerBatch b = new PersonAccountAnalyzerBatch(theQuery);
database.executebatch(b, 1);
*/
```


# Last Modified


# Usage

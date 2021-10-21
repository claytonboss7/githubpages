---
layout: default
title: BT_Utils
parent: classes
---
# Metadata Type
classes


# Filename 
BT_Utils


# Raw XML
```
/**
 * @description       : 
 * @author            : sfdc cb
 * @group             : 
 * @last modified on  : 10-02-2021
 * @last modified by  : sfdc cb
**/
public with sharing class BT_Utils {
    public BT_Utils() {

    }

    public static void sendEmailUpdate(){
        Messaging.SingleEmailMessage message = new Messaging.SingleEmailMessage();
        message.toAddresses = new String[] { 'recipient@email.com'};
        message.subject = 'subject';
        message.plainTextBody = 'subject';
        Messaging.SingleEmailMessage[] messages = new List<Messaging.SingleEmailMessage> {message};
        Messaging.SendEmailResult[] results = Messaging.sendEmail(messages);
        if (results[0].success) {
            System.debug('The email was sent successfully.');
        } else{
            System.debug('The email failed to send: ' + results[0].errors[0].message);
        }
    }

    public static void postToSlack(String theMessage){
      // SlackWebApi.postMessage(new List<SlackWebApi.SlackMessage>{new SlackWebApi.SlackMessage('G01G2P4UCCW',theMessage)});
    }
    public static void postToSlack(String theChannel, String theMessage){
       // SlackWebApi.postMessage(new List<SlackWebApi.SlackMessage>{new SlackWebApi.SlackMessage(theChannel,theMessage)});
     }
}
```


# Last Modified


# Usage

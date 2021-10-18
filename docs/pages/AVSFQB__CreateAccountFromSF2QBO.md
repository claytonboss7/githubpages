---
layout: default
title: AVSFQB__CreateAccountFromSF2QBO
parent: pages
---

```<apex:page standardcontroller="Account">
    <apex:form style="align:center;text-align:center">
        <apex:sectionHeader title="Salesforce QuickBooksOnline Integration" />
        <script>
        <!-- Creation of Customer -->
    
        function createAccount() {
            var URL = "{!$User.AVSFQB__QBOE_DBSync_Server__c}/qboe.m?sfUrl={!$Api.Partner_Server_URL_140}&qboeCT={!$User.AVSFQB__QBOE_Connection_Ticket__c}&pdl=processdefinition_SFQB_Account.xml&recordId={!Account.Id}&dbsyncId={!$User.AVSFQB__DBSync_Id__c}&profileName={!$User.AVSFQB__DBSync_Profile__c}&sessionId={!$Api.Session_ID}&dbsyncPasswd={!$User.AVSFQB__DBSync_Passwd__c}";
            window.open(URL, "DBSync",
                    "menubar=0,resizable=0,width=650,height=300");
        }
        
    </script>
        <apex:commandButton value="Create Accounts in QBO" id="theButton1"
            onclick="createAccount()"
            style="margin:10px;font-size:15px;padding:10px;" />
    </apex:form>
</apex:page>```

---
layout: default
title: Dashboard_SearchBoxController
parent: classes
---
# Metadata Type
classes


# Filename 
Dashboard_SearchBoxController


# Raw XML
```
global class Dashboard_SearchBoxController {
    @RemoteAction
    global static String searchProd(String query, Boolean all){
        query = '%' + query + '%';
        List<wrapperDataProd> prodList = new List<wrapperDataProd>();
        List<Opportunity> productionList;
        if(!all) productionList = [SELECT Id, Name, Alias_With_Production_Name__c, StageName, Office_Location__c, Company__c FROM Opportunity WHERE Alias_with_Production_Name__c LIKE: query AND StageName = 'Active' LIMIT 10];
        else productionList = [SELECT Id, Name, Alias_With_Production_Name__c, StageName, Office_Location__c, Company__c FROM Opportunity WHERE Alias_with_Production_Name__c LIKE: query LIMIT 10];
        for(Opportunity o : productionList){
            prodList.add(new wrapperDataProd(o.Id,o.Alias_With_Production_Name__c,o.StageName,o.Company__c != null ? o.Company__c : '',o.Office_Location__c != null ? o.Office_Location__c : ''));
        }
        return JSON.serialize(prodList);
    }
    
    global class wrapperDataProd {
        public String data;
        public String value;
        public String extra1;
        public String extra2;
        public String extra3;
        
        public wrapperDataProd(String cdata, String cvalue, String cextra1, String cextra2, String cextra3){
            data = cdata;
            value = cvalue;
            extra1 = cextra1;
            extra2 = cextra2;
            extra3 = cextra3;
        }
    }
}
```


# Last Modified


# Usage

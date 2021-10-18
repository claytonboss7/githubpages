---
layout: default
title: ProductionAssociationsTrigger
parent: triggers
---

```trigger ProductionAssociationsTrigger on Production_Associations__c (before insert, before update) {
    if(trigger.isInsert){
        Map<String,List<String>> prodMap = new Map<String,List<String>>();
        List<String> listAux;
        for(Production_Associations__c pa : trigger.new){
            if(pa.Production_Opp__c != null && pa.Team_Roles__c != null){
                listAux = pa.Team_Roles__c.split(';');
                prodMap.put(pa.Production_Opp__c,listAux.clone());
            }
        }
        
        system.debug(prodMap);
        if(!prodMap.isEmpty()){
            List<Production_Associations__c> oppAssocList = [SELECT Id, Production_Opp__c, Team_Roles__c FROM Production_Associations__c WHERE Production_Opp__c IN: prodMap.keySet() AND Team_Roles__c <> NULL];
            
            for(Production_Associations__c pa : trigger.new){
                if(pa.Production_Opp__c != null && pa.Team_Roles__c != null){
                    for(Production_Associations__c paData : oppAssocList){
                        if(pa.Production_Opp__c == paData.Production_Opp__c && prodMap.get(pa.Production_Opp__c) != null){
                            for(String roleData : paData.Team_Roles__c.split(';')){
                                for(String role : pa.Team_Roles__c.split(';')){
                                    system.debug(roleData + ' - ' + role);
                                    if(role == roleData && role.contains('Primary Housing')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary GT')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary Air')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary Freight')) pa.addError('It cannot have two primary coordinators.');
                                }
                            }
                        }
                    }
                }
            }
        }
    }else{
        Map<String,List<String>> prodMap = new Map<String,List<String>>();
        List<String> listAux;
        for(Production_Associations__c pa : trigger.new){
            if(pa.Production_Opp__c != null && pa.Team_Roles__c != null){
                listAux = pa.Team_Roles__c.split(';');
                prodMap.put(pa.Production_Opp__c,listAux.clone());
            }
        }
        
        system.debug(prodMap);
        if(!prodMap.isEmpty()){
            List<Production_Associations__c> oppAssocList = [SELECT Id, Production_Opp__c, Team_Roles__c FROM Production_Associations__c WHERE Production_Opp__c IN: prodMap.keySet() AND Team_Roles__c <> NULL];
            
            for(Production_Associations__c pa : trigger.new){
                if(pa.Production_Opp__c != null && pa.Team_Roles__c != null){
                    for(Production_Associations__c paData : oppAssocList){
                        if(pa.Production_Opp__c == paData.Production_Opp__c && prodMap.get(pa.Production_Opp__c) != null && pa.Id != paData.Id){
                            for(String roleData : paData.Team_Roles__c.split(';')){
                                for(String role : pa.Team_Roles__c.split(';')){
                                    system.debug(roleData + ' - ' + role);
                                    if(role == roleData && role.contains('Primary Housing')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary GT')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary Air')) pa.addError('It cannot have two primary coordinators.');
                                    if(role == roleData && role.contains('Primary Freight')) pa.addError('It cannot have two primary coordinators.');
                                }
                            }
                        }
                    }
                }
            }
        }
    }
    
}```

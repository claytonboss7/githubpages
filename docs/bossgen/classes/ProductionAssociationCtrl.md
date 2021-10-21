---
layout: default
title: ProductionAssociationCtrl
parent: classes
---
# Metadata Type
classes


# Filename 
ProductionAssociationCtrl


# Raw XML
```
public class ProductionAssociationCtrl {
	
    @AuraEnabled
    public static String getOpportunityId(String prodAssId) {
        return [Select Production_Opp__c from Production_Associations__c where Id =: prodAssId].Production_Opp__c;
    }
}
```


# Last Modified


# Usage

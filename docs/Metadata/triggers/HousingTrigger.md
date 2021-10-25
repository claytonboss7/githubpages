---
layout: default
title: HousingTrigger
parent: triggers
grand_parent: Metadata
---
# Metadata Type
triggers


# Filename 
HousingTrigger


# Raw XML
```
trigger HousingTrigger on Housing__c(
  before insert,
  before update,
  before delete,
  after insert,
  after update,
  after delete,
  after undelete
) {
  TriggerDispatcher.Run(new HousingTriggerHandler(), Trigger.operationType);
}
```


# Last Modified


# Usage

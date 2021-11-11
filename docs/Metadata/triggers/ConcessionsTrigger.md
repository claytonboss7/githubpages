---
layout: default
title: ConcessionsTrigger
parent: triggers
grand_parent: Metadata
---
# Metadata Type
triggers


# Filename 
ConcessionsTrigger


# Raw XML
```
trigger ConcessionsTrigger on Concessions__c(
  before insert,
  before update,
  before delete,
  after insert,
  after update,
  after delete,
  after undelete
) {
  TriggerDispatcher.Run(new ConcessionsTriggerHandler(), Trigger.operationType);
}
```


# Last Modified


# Usage

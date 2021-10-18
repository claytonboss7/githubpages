---
layout: default
title: HousingTrigger
parent: triggers
---

```trigger HousingTrigger on Housing__c(
  before insert,
  before update,
  before delete,
  after insert,
  after update,
  after delete,
  after undelete
) {
  TriggerDispatcher.Run(new HousingTriggerHandler(), Trigger.operationType);
}```

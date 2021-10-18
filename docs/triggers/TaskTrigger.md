---
layout: default
title: TaskTrigger
parent: triggers
---

```trigger TaskTrigger on Task(
  before insert,
  before update,
  before delete,
  after insert,
  after update,
  after delete,
  after undelete
) {
  TriggerDispatcher.Run(new TaskTriggerHandler(), Trigger.operationType);
}```

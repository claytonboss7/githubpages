---
layout: default
title: TaskTrigger
parent: triggers
grand_parent: Metadata
---
# Metadata Type
triggers


# Filename 
TaskTrigger


# Raw XML
```
trigger TaskTrigger on Task(
  before insert,
  before update,
  before delete,
  after insert,
  after update,
  after delete,
  after undelete
) {
  TriggerDispatcher.Run(new TaskTriggerHandler(), Trigger.operationType);
}
```


# Last Modified


# Usage

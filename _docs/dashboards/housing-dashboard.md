---
title: Housing Dashboard
description: Details on Housing Dashboard
---

# Dashboards

There are 4 similar dashboards for all of the services that get serviced.   Housing is the focus at the time of writing and the GT, Freight, and Air ones are similar with their own little nuances.  These details will try and give a user overview as well as a training for the business logic that lives in the code,  as it will be laid out in the details on the page.  This can hopefully be a reference to anyone who has to reference parts of the workflow whether it is for a new hire or internally to spread the knowledge.

## Housing Dashboard
Housing is the pilot service and where the largest chunk of effort has gone into.  Housing would have some key details on the setup of the Housing Objects and the Production, and how default preferred Room Types are stored and related to everything properly.  From a user perspective, the Housing Dashboard is where Coordinators will work Productions that are Active and the Coordinators will facilitate everything that goes into booking their travel.  The process starts with some key objects:

* Production
* Production Association
* Housing__c (Sales Housing)
* Housing__c (Hotel Housing/IR/Corp)
* Housing__c (Room Types and Ops [Sales Housing])
* Housing__c (Room Types and Ops [Bid Room Rate])
* Bid record

Production > Sales Housing Room Types and Ops > Hotel Housing > Bid > Room Types and Ops

You can see in this drawing how the objects relate to eachother and how they interconnect:
datamodel

### Housing Details

* Functional Actions
  * View / Search / Add Production Journals
  * Add new Room Types to Sales Housing
    * (These are now "preloaded?")
* Underlying Data / Objects
* Custom Logic
* View room type data
  * (Units / Unit Type / Special Notes / )
  * EDIT and DELETE records
* Add New Concession
  * Concession Specifics NEEDED!
* Contracting Requirements load based on criteria
* Billing Options drop down populate with criteria
* Budget populated
* Deadline Trace is set
---
title: Bid Submission Landing Page
description: Diagrams and Documentation for Bid Submission Landing Page.
---

## Bid Submission Landing Page

### Overview
When a stay is being worked by a Coordinator, they need to choose a Vendor and hotel to setup as a Bid that will be submitted by the vendor.  The original bid submit process happened in the Community under an Authenticated User, and this new method uses Force.com sites and a Public facing landing page to collect the bid data, and offer PDFs to the Vendor to download.  The goal was to reduce licensing costs if possible, and this got rid of the need for the Community Licenses.

### Business Process
- Update the Bid with details Vendor enters
- Update the Revenue record (Room Commission)
- Save Vendor note as Concession
- Update Rate on Room Type Housing Records
- Save Journal entry related to Bid Submit
- Create Bid Memorialization 

### Process Flow
<div style="width: 640px; height: 480px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" src="https://lucid.app/documents/embeddedchart/f45d427d-740d-4241-9c5c-e670d8aeb3b1" id="R8wNAV.UpBU-"></iframe></div>

### 5 Ws

### Technical Details
#### Salesforce Objects
- Bid
- Housing
- Revenue
- Concessions

### References
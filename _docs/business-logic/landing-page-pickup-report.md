---
title: Pickup Report Landing Page
description: Diagrams and Documentation for Pickup Report Landing Page.
---

# Pickup Report Landing Page

## Overview
Pickup Report is sent to Vendor to submit details about the stay and confirm the Room Nights and Rate Information is correct.  After submitting the pickup report, the Revenue records and Room Types housing records are "Closed out" and updated with the final numbers for the Stay.

## Business Process
- Save the Close out Room details on the Housing record
- Update Revenue Room Record with all of the data from the Pick Up submission
- Update Revenue record with Rebate/Commission/Service Fees data
- Update Bid with Close Out Flag
- Create trace for Coordinator (or Frontend B.E. Coordinator) for Vendor Submitted Data
- Save Journal entry related to Bid Submit
- Create Pickup Report PDF and attach to bid

## Process Flow

<div style="width: 960px; height: 720px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:960px; height:720px" src="https://lucid.app/documents/embeddedchart/362a79fb-0fcb-431a-88cb-40b093f416cd" id="MiHNXPorOnlz"></iframe></div>

## 5 Ws
- Who:  Vendors submitting final Room data after a Stay is complete
- What: A Landing Page where Pick Up details could be viewed/edited/submitted
- Where:  Force.com Sites in Salesforce hosted as Public facing sites
- When:  Vendors will utilize when they receive a Pick Up Report submit request submitted by the Coordinator with the "Pick Up Report" button in the Contracting tab.
- Why:  We needed a way to get input from Vendors that integrate directly with Salesforce to facilitate the submission of Pickup Reports.

## Technical Details
### Salesforce Objects
- Bid
- Housing
- Revenue
- Concessions

### References
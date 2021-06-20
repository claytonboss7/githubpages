---
title: Pickup Report Landing Page
description: Diagrams and Documentation for Pickup Report Landing Page.
---

# Bid Submission Landing Page

## Overview
Pickup Report is sent to Vendor to submit details about the stay and confirm the Room Nights and Rate Information is correct.  After submitting the pickup report, the Revenue records and Room Types housing records are "Closed out" and updated with the final numbers for the Stay.

## Business Process
- Update the Bid with details Vendor enters
- Update the Revenue record (Room Commission)
- Save Vendor note as Concession
- Update Rate on Room Type Housing Records
- Save Journal entry related to Bid Submit
- Create Bid Memorialization PDF

## Process Flow

<div style="width: 960px; height: 720px; margin: 10px; position: relative;"><iframe allowfullscreen frameborder="0" style="width:960px; height:720px" src="https://lucid.app/documents/embeddedchart/f45d427d-740d-4241-9c5c-e670d8aeb3b1" id="VWGN5N_fVjcK"></iframe></div>

## 5 Ws
- Who:  Vendors submitting Bids will use the Landing Pages to submit Bids the Coordinators sent to them
- What: Landing Pages for Vendor management functions for Bid Submits and Pickup Reports
- Where:  Force.com Sites in Salesforce hosted as Public facing sites
- When:  Vendors will utilize when they receive a Bid Submission Request or a Pick Up Report submit request.
- Why:  We needed a way to get input from Vendors that integrate directly with Salesforce to facilitate the Bids for customers Room requests.

## Technical Details
### Salesforce Objects
- Bid
- Housing
- Revenue
- Concessions

### References
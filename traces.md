# Traces

Traces are a unit of work used to track a date for an event in the workflow, that a Coordinator would have to track and complete. The automation of the dates and when it completes is listed below as well as the different statuses and trace subjects that are in the system.

## Housing

Traces are created using the Primary Contract Coordinator, and triggered when the Housing Contract is sent out. This datestamp that Conga does at the end of its workflow to the "Housing Contract Last Send Date" field is what the trigger is watching for to create the traces. Based on the **Record Type** of the Housing, it will create a number of traces.

### Record Type - Hotel Housing

- PENDING_CONTRACT,
- NEEDS_PROOFING,
- PENDING_REVISED_CONTRACT,
- NEED_TO_SEND_TO_CLIENT,
- PENDING_CLIENT_SIGNATURE,
- PENDING_CLIENT_CHOICE,
- PENDING_HOTEL_COUNTER,
- PENDING_DATE_CHANGE,
- PENDING_UPDATE,
- PENDING_NO_ROOMS_PICKED_UP,
- PENDING_CANCELLATION,
- CREATE_GCIP,
- AWAITING_GCIP,
- ROOMING_LIST_REMINDER,
- CONTRACT_DUE_DATE,
- ROOMING_LIST_DUE_DATE,
- AWAITING_ADDENDUM,
- AWAITING_PICK_UP,
- AWAITING_BILLING,
- PENDING_ISSUE,
- CHECK_IN_CALL,
- PENDING_COMMISSION_TRACE

### Record Type - Individual Reservation

- AWAITING_CONFIRMATION_NUMBERS,
- AWAITING_BILLING,
- PENDING_RATE_AGREEMENT,
- CHECK_IN_CALL,
- CHECK_OUT_CALL,
- PENDING_ISSUE,
- PENDING_COMMISSION_TRACE

### Record Type - Corporate Housing

- PENDING_RATE_AGREEMENT,
- NEEDS_PROOFING,
- PENDING_REVISED,
- NEEDS_TO_SEND_TO_CLIENT,
- PENDING_UPDATE,
- AWAITING_ADDENDUM,
- PENDING_CANCELLATION,
- ROOMING_LIST_REMINDER,
- ROOMING_LIST_DUE_DATE,
- PENDING_ISSUE,
- AWAITING_BILLING,
- PENDING_DATE_CHANGE,
- CHECK_IN_CALL,
- AWAITING_PICK_UP,
- PENDING\*COMMISSION_TRACE

  ## Trace Reassignment

  The statuses for Housing on the **Front End** (StatusCC picklist) each have a task assigned to them if set with a trace date. In siutuations where a **Front End Coordinator** \*(Primary Housing Coordinator)\_ and **Backend Coordinator** are set, only certain statuses should be assigned to the **Backend Coordinator** to handle. The sheet below lists each status and if it should be reassigned when the **Back end Coordinator** is set. It also will assign back to **Primary Housing Coordinator** if the backend is removed.

### Google Sheet - Trace Reassignment

[source:: Google Sheet](https://docs.google.com/spreadsheets/d/e/2PACX-1vTI3TAuXXMfal6AoPo7221t9A_fh23pRSvjC1cz2DTy_riyDAemixLec23V4IEuA-HNLR0H8NipiOI2/pubhtml)

<iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTI3TAuXXMfal6AoPo7221t9A_fh23pRSvjC1cz2DTy_riyDAemixLec23V4IEuA-HNLR0H8NipiOI2/pubhtml?widget=true&amp;headers=false" height="700" width="600"></iframe>

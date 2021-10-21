---
layout: default
title: TraceDashboardController
parent: classes
---
# Metadata Type
classes


# Filename 
TraceDashboardController


# Raw XML
```
global class TraceDashboardController {
  public Date searchStartDate { get; set; }
  public Date searchEndDate { get; set; }
  public static String searchSortBy { get; set; }
  public Boolean searchAllCoordinators { get; set; }
  public String[] searchCoordinator { get; set; }
  public List<SelectOption> searchCoordinatorPL { get; set; }
  public String searchTraceType { get; set; }
  public Boolean searchAllStatus { get; set; }
  public String[] searchStatus { get; set; }
  public List<SelectOption> searchStatusPL { get; set; }
  public Set<String> allSubjectsSet { get; set; }
  public String[] searchService { get; set; }
  public Boolean searchUrgentTaskOnly { get; set; }

  //search result lists
  public Map<Id, Housing__c> housingMap { get; set; }
  public Map<Id, Housing__c> housingMapDeadlines { get; set; }
  public Map<Id, Bid__c> bidMap_housing { get; set; }
  public List<Task> lsAuditTrace_Housing { get; set; }
  public List<Journal__c> lsJournals_Housing { get; set; }
  public List<Housing__c> lsTraces_Housing { get; set; }
  public Integer lsAuditTrace_Housing_limit { get; set; }
  public Integer lsJournals_Housing_limit { get; set; }
  public Boolean loadAllContractTraces_Housing_showBtn { get; set; }

  public Map<String, String> proCoordinatorMap { get; set; }
  public Set<String> whatStatusToSearch { get; set; }

  public Map<Id, Ground__c> gtMap { get; set; }
  public Map<Id, Bid__c> bidMap_GT { get; set; }
  public List<Task> lsAuditTrace_GT { get; set; }
  public List<Journal__c> lsJournals_GT { get; set; }
  public List<Ground__c> lsTraces_GT { get; set; }
  public Integer lsAuditTrace_GT_limit { get; set; }
  public Integer lsJournals_GT_limit { get; set; }

  public Map<Id, Freight__c> freightMap { get; set; }
  public Map<Id, Bid__c> bidMap_Freight { get; set; }
  public List<Task> lsAuditTrace_Freight { get; set; }
  public List<Journal__c> lsJournals_Freight { get; set; }
  public List<Freight__c> lsTraces_Freight { get; set; }
  public Integer lsAuditTrace_Freight_limit { get; set; }
  public Integer lsJournals_Freight_limit { get; set; }

  public Map<Id, Air__c> airMap { get; set; }
  public Map<Id, Bid__c> bidMap_Air { get; set; }
  public List<Task> lsAuditTrace_Air { get; set; }
  public List<Journal__c> lsJournals_Air { get; set; }
  public List<Air__c> lsTraces_Air { get; set; }
  public Integer lsAuditTrace_Air_limit { get; set; }
  public Integer lsJournals_Air_limit { get; set; }

  public Map<Id, Bid__c> bidMap_AllOther { get; set; }
  public List<Task> lsAuditTrace_AllOther { get; set; }
  public List<Journal__c> lsJournals_AllOther { get; set; }
  public List<Task> lsTrace_AllOther { get; set; }
  public Integer lsTrace_AllOther_limit { get; set; }

  public List<TaskWrapper> lsTraceDeadlineDate_Housing { get; set; }
  public List<TaskWrapper> lsTraceNoContract_Housing { get; set; }
  public List<TaskWrapper> lsTraceNoContract_GT { get; set; }
  public List<TaskWrapper> lsTraceNoContract_Freight { get; set; }
  public List<TaskWrapper> lsTraceNoContract_Air { get; set; }

  public List<GroupTasksWrapper> lsGroupsTWNoContractDeadlineDate_Housing { get; set; }
  public List<GroupTasksWrapper> lsGroupsTWNoContract_Housing { get; set; }
  public List<GroupTasksWrapper> lsGroupsTWNoContract_GT { get; set; }
  public List<GroupTasksWrapper> lsGroupsTWNoContract_Freight { get; set; }
  public List<GroupTasksWrapper> lsGroupsTWNoContract_Air { get; set; }

  public List<TaskWrapper> lsTraceContract_Housing { get; set; }
  public List<TaskWrapper> lsTraceContractDeadlineDate_Housing { get; set; }
  public List<TaskWrapper> lsTraceContract_GT { get; set; }
  public List<TaskWrapper> lsTraceContract_Freight { get; set; }
  public List<TaskWrapper> lsTraceContract_Air { get; set; }

  public List<GroupTasksWrapper> lsGroupsTW_Housing_AllOther { get; set; }
  public List<GroupTasksWrapper> lsGroupsTW_GT_AllOther { get; set; }
  public List<GroupTasksWrapper> lsGroupsTW_Freight_AllOther { get; set; }
  public List<GroupTasksWrapper> lsGroupsTW_Air_AllOther { get; set; }

  public Integer item_number { get; set; }
  public String sortListBy { get; set; }

  public TraceDashboardController(ApexPages.StandardController standardController) {
    system.debug('## TraceDashboardController(ApexPages..)');
    Init();
  }

  public TraceDashboardController() {
    system.debug('## TraceDashboardController()');
    Init();
  }

  public void Init() {
    system.debug('## TraceDashboardController - Init()');

    searchStartDate = Date.today().addDays(-2);
    searchEndDate = Date.today();
    searchSortBy = 'By Status';
    searchAllCoordinators = false;
    searchCoordinator = new List<String>();

    //set searchCoordinatorPL
    searchCoordinatorPL = new List<SelectOption>();
    for (
      User u : [
        SELECT Id, Name
        FROM User
        WHERE IsActive = TRUE AND Profile.Name != 'Road Rebel Vendor' AND Profile.Name != 'Road Rebel Customer'
        ORDER BY Name ASC
      ] //IsActive = true?
    )
      searchCoordinatorPL.add(new SelectOption(u.id, u.name));
    //end set

    /* clay to add filter down on the correct coordinators */

    searchTraceType = ''; ///considerar establecer default
    searchAllStatus = false;
    searchStatus = new List<String>();
    searchUrgentTaskOnly = false;

    //set searchStatusPL
    searchStatusPL = new List<SelectOption>();
    /*searchStatusPL.add(new SelectOption('Acknowledgement of Contract', 'Acknowledgement of Contract'));
        searchStatusPL.add(new SelectOption('Air Travel Itinerary Received in Community', 'Air Travel Itinerary Received in Community'));
        searchStatusPL.add(new SelectOption('Awaiting Addendum', 'Awaiting Addendum'));
        searchStatusPL.add(new SelectOption('Awaiting Billing', 'Awaiting Billing'));
        searchStatusPL.add(new SelectOption('Awaiting Confirmation Numbers', 'Awaiting Confirmation Numbers'));
        searchStatusPL.add(new SelectOption('Awaiting GCIP', 'Awaiting GCIP'));
        searchStatusPL.add(new SelectOption('Awaiting Pick-Up', 'Awaiting Pick-Up'));
        searchStatusPL.add(new SelectOption('Awaiting Trip Info', 'Awaiting Trip Info'));
        searchStatusPL.add(new SelectOption('Bid Request Stage', 'Bid Request Stage'));
        searchStatusPL.add(new SelectOption('Budgeting', 'Budgeting'));
        searchStatusPL.add(new SelectOption('Booked - Confirmed', 'Booked - Confirmed'));
        searchStatusPL.add(new SelectOption('Cancelled', 'Cancelled'));
        searchStatusPL.add(new SelectOption('Check-in Call', 'Check-in Call'));
        searchStatusPL.add(new SelectOption('Check-out Call', 'Check-out Call'));
        searchStatusPL.add(new SelectOption('Confirmation Numbers Sent to Client', 'Confirmation Numbers Sent to Client'));
        searchStatusPL.add(new SelectOption('Confirmation Email', 'Confirmation Email'));
        searchStatusPL.add(new SelectOption('Contract Due Date', 'Contract Due Date'));
        searchStatusPL.add(new SelectOption('Contracted', 'Contracted'));
        searchStatusPL.add(new SelectOption('Contracted on Own', 'Contracted on Own'));
        searchStatusPL.add(new SelectOption('Client Choose Option', 'Client Choose Option'));
        searchStatusPL.add(new SelectOption('Create GCIP', 'Create GCIP'));
        searchStatusPL.add(new SelectOption('Decision Due Date reminder', 'Decision Due Date reminder'));
        searchStatusPL.add(new SelectOption('Deposit Due', 'Deposit Due'));
        searchStatusPL.add(new SelectOption('Deposit Reminder', 'Deposit Reminder'));
        searchStatusPL.add(new SelectOption('Email Confirmation', 'Email Confirmation'));
        searchStatusPL.add(new SelectOption('Enter Itinerary Pending', 'Enter Itinerary Pending'));
        searchStatusPL.add(new SelectOption('FCQ ', 'FCQ '));
        searchStatusPL.add(new SelectOption('Final Follow-up', 'Final Follow-up'));
        searchStatusPL.add(new SelectOption('Freight receiver contact details', 'Freight receiver contact details'));
        searchStatusPL.add(new SelectOption('Freight Travel Itinerary Received in Community', 'Freight Travel Itinerary Received in Community'));
        searchStatusPL.add(new SelectOption('GCQ', 'GCQ'));
        searchStatusPL.add(new SelectOption('GCQ Call', 'GCQ Call'));
        searchStatusPL.add(new SelectOption('Ground Travel Itinerary Received in Community', 'Ground Travel Itinerary Received in Community'));
        searchStatusPL.add(new SelectOption('In Contracting', 'In Contracting'));
        searchStatusPL.add(new SelectOption('Initial Follow-up', 'Initial Follow-up'));
        searchStatusPL.add(new SelectOption('Itinerary Received', 'Itinerary Received'));
        searchStatusPL.add(new SelectOption('Layoff', 'Layoff'));
        searchStatusPL.add(new SelectOption('Lodging Itinerary Received in Community', 'Lodging Itinerary Received in Community'));
        searchStatusPL.add(new SelectOption('Manifest', 'Manifest'));
        searchStatusPL.add(new SelectOption('Names & Final Payment Due', 'Names & Final Payment Due'));
        searchStatusPL.add(new SelectOption('Names & Final Payment Reminder', 'Names & Final Payment Reminder'));
        searchStatusPL.add(new SelectOption('Need to Send to Client', 'Need to Send to Client'));
        searchStatusPL.add(new SelectOption('Needs Proofing', 'Needs Proofing'));
        searchStatusPL.add(new SelectOption('Needs to Send to Client', 'Needs to Send to Client'));
        searchStatusPL.add(new SelectOption('Passenger List', 'Passenger List'));
        searchStatusPL.add(new SelectOption('Pending Airport Confirmation', 'Pending Airport Confirmation'));
        searchStatusPL.add(new SelectOption('Pending Client Choice', 'Pending Client Choice'));
        searchStatusPL.add(new SelectOption('Pending Confirmation Numbers', 'Pending Confirmation Numbers'));
        searchStatusPL.add(new SelectOption('Pending Trip Information', 'Pending Trip Information'));
        searchStatusPL.add(new SelectOption('Pending Cancellation', 'Pending Cancellation'));
        searchStatusPL.add(new SelectOption('Pending Client Signature', 'Pending Client Signature'));
        searchStatusPL.add(new SelectOption('Pending Commission Trace', 'Pending Commission Trace'));
        searchStatusPL.add(new SelectOption('Pending Contract', 'Pending Contract'));
        searchStatusPL.add(new SelectOption('Pending Counter', 'Pending Counter'));
        searchStatusPL.add(new SelectOption('Pending Date Change', 'Pending Date Change'));
        searchStatusPL.add(new SelectOption('Pending Hotel Counter', 'Pending Hotel Counter'));
        searchStatusPL.add(new SelectOption('Pending Issue', 'Pending Issue'));
        searchStatusPL.add(new SelectOption('Pending No Rooms Picked Up', 'Pending No Rooms Picked Up'));
        searchStatusPL.add(new SelectOption('Pending Rate Agreement', 'Pending Rate Agreement'));
        searchStatusPL.add(new SelectOption('Pending Revised', 'Pending Revised'));
        searchStatusPL.add(new SelectOption('Pending Revised Contract', 'Pending Revised Contract'));
        searchStatusPL.add(new SelectOption('Pending Trip Update', 'Pending Trip Update'));
        searchStatusPL.add(new SelectOption('Pending Update', 'Pending Update'));
        searchStatusPL.add(new SelectOption('Presenter Provided', 'Presenter Provided'));
        searchStatusPL.add(new SelectOption('Presenter/Promoter Provided', 'Presenter/Promoter Provided'));
        searchStatusPL.add(new SelectOption('Ready to Invoice', 'Ready to Invoice'));
        searchStatusPL.add(new SelectOption('Review Pick up Report', 'Review Pick up Report'));
        searchStatusPL.add(new SelectOption('Rework', 'Rework'));
        searchStatusPL.add(new SelectOption('Rooming List Due Date', 'Rooming List Due Date'));
        searchStatusPL.add(new SelectOption('Rooming List Reminder', 'Rooming List Reminder'));
        searchStatusPL.add(new SelectOption('RT Awaiting Trip Info', 'RT Awaiting Trip Info'));
        searchStatusPL.add(new SelectOption('RT Confirmation Email', 'RT Confirmation Email'));
        searchStatusPL.add(new SelectOption('RT FCQ', 'RT FCQ'));
        searchStatusPL.add(new SelectOption('RT GCQ', 'RT GCQ'));
        searchStatusPL.add(new SelectOption('Schedule Changes', 'Schedule Changes'));
        searchStatusPL.add(new SelectOption('Send to Client', 'Send to Client'));
        searchStatusPL.add(new SelectOption('Shuttling', 'Shuttling'));
        searchStatusPL.add(new SelectOption('Tentative Dates', 'Tentative Dates'));
        searchStatusPL.add(new SelectOption('Ticketed Confirmation', 'Ticketed Confirmation'));
        searchStatusPL.add(new SelectOption('Travel Dates', 'Travel Dates'));
        searchStatusPL.add(new SelectOption('Utilization Date', 'Utilization Date'));
        searchStatusPL.add(new SelectOption('Utilization Reminder', 'Utilization Reminder'));
        searchStatusPL.add(new SelectOption('Vendor Submitted Close out report', 'Vendor Submitted Close out report'));
        
        allSubjectsSet = new Set<String>();
        for(SelectOption so : searchStatusPL)
            allSubjectsSet.add(so.getValue());*/

    //TEST-120820
    List<SelectOption> selectOptions = new List<SelectOption>();
    Map<String, String> plValueLabels = picklistValues('Housing__c', 'Status_CC__c');
    //aux put options
    plValueLabels.put('Acknowledgement of Contract', 'Acknowledgement of Contract');
    plValueLabels.put('Air Travel Itinerary Received in Community', 'Air Travel Itinerary Received in Community');
    plValueLabels.put('Awaiting Addendum', 'Awaiting Addendum');
    plValueLabels.put('Awaiting Billing', 'Awaiting Billing');
    plValueLabels.put('Awaiting Confirmation Numbers', 'Awaiting Confirmation Numbers');
    plValueLabels.put('Awaiting GCIP', 'Awaiting GCIP');
    plValueLabels.put('Awaiting Pick-Up', 'Awaiting Pick-Up');
    plValueLabels.put('Reservation Cut Off Date', 'Reservation Cut Off Date');
    plValueLabels.put('Update Booking Site', 'Update Booking Site');
    plValueLabels.put('Proof Booking Link', 'Proof Booking Link');
    plValueLabels.put('Pending Booking Link', 'Pending Booking Link');
    plValueLabels.put('Post Report to Client', 'Post Report to Client');
    plValueLabels.put('Awaiting Trip Info', 'Awaiting Trip Info');
    plValueLabels.put('Bid Request Stage', 'Bid Request Stage');
    plValueLabels.put('Budgeting', 'Budgeting');
    plValueLabels.put('Booked - Confirmed', 'Booked - Confirmed');
    plValueLabels.put('Cancelled', 'Cancelled');
    plValueLabels.put('Check-in Call', 'Check-in Call');
    plValueLabels.put('Check-out Call', 'Check-out Call');
    plValueLabels.put('Confirmation Numbers Sent to Client', 'Confirmation Numbers Sent to Client');
    plValueLabels.put('Confirmation Email', 'Confirmation Email');
    plValueLabels.put('Contract Due Date', 'Contract Due Date');
    plValueLabels.put('Contracted', 'Contracted');
    plValueLabels.put('Contracted on Own', 'Contracted on Own');
    plValueLabels.put('Client Choose Option', 'Client Choose Option');
    plValueLabels.put('Create GCIP', 'Create GCIP');
    plValueLabels.put('Decision Due Date reminder', 'Decision Due Date reminder');
    plValueLabels.put('Deposit Due', 'Deposit Due');
    plValueLabels.put('Deposit Reminder', 'Deposit Reminder');
    plValueLabels.put('Email Confirmation', 'Email Confirmation');
    plValueLabels.put('Enter Itinerary Pending', 'Enter Itinerary Pending');
    plValueLabels.put('FCQ ', 'FCQ ');
    plValueLabels.put('Final Follow-up', 'Final Follow-up');
    plValueLabels.put('Freight receiver contact details', 'Freight receiver contact details');
    plValueLabels.put(
      'Freight Travel Itinerary Received in Community',
      'Freight Travel Itinerary Received in Community'
    );
    plValueLabels.put('GCQ', 'GCQ');
    plValueLabels.put('GCQ Call', 'GCQ Call');
    plValueLabels.put('Ground Travel Itinerary Received in Community', 'Ground Travel Itinerary Received in Community');
    plValueLabels.put('In Contracting', 'In Contracting');
    plValueLabels.put('Initial Follow-up', 'Initial Follow-up');
    plValueLabels.put('Itinerary Received', 'Itinerary Received');
    plValueLabels.put('Layoff', 'Layoff');
    plValueLabels.put('Lodging Itinerary Received in Community', 'Lodging Itinerary Received in Community');
    plValueLabels.put('Manifest', 'Manifest');
    plValueLabels.put('Names & Final Payment Due', 'Names & Final Payment Due');
    plValueLabels.put('Names & Final Payment Reminder', 'Names & Final Payment Reminder');
    plValueLabels.put('Need to Send to Client', 'Need to Send to Client');
    plValueLabels.put('Needs Proofing', 'Needs Proofing');
    plValueLabels.put('Needs to Send to Client', 'Needs to Send to Client');
    plValueLabels.put('Passenger List', 'Passenger List');
    plValueLabels.put('Pending Airport Confirmation', 'Pending Airport Confirmation');
    plValueLabels.put('Pending Client Choice', 'Pending Client Choice');
    plValueLabels.put('Pending Confirmation Numbers', 'Pending Confirmation Numbers');
    plValueLabels.put('Pending Trip Information', 'Pending Trip Information');
    plValueLabels.put('Pending Cancellation', 'Pending Cancellation');
    plValueLabels.put('Pending Client Signature', 'Pending Client Signature');
    plValueLabels.put('Pending Commission Trace', 'Pending Commission Trace');
    plValueLabels.put('Pending Contract', 'Pending Contract');
    plValueLabels.put('Pending Counter', 'Pending Counter');
    plValueLabels.put('Pending Date Change', 'Pending Date Change');
    plValueLabels.put('Pending Hotel Counter', 'Pending Hotel Counter');
    plValueLabels.put('Pending Issue', 'Pending Issue');
    plValueLabels.put('Pending No Rooms Picked Up', 'Pending No Rooms Picked Up');
    plValueLabels.put('Pending Rate Agreement', 'Pending Rate Agreement');
    plValueLabels.put('Pending Revised', 'Pending Revised');
    plValueLabels.put('Pending Revised Contract', 'Pending Revised Contract');
    plValueLabels.put('Pending Trip Update', 'Pending Trip Update');
    plValueLabels.put('Pending Update', 'Pending Update');
    plValueLabels.put('Presenter Provided', 'Presenter Provided');
    plValueLabels.put('Presenter/Promoter Provided', 'Presenter/Promoter Provided');
    plValueLabels.put('Ready to Invoice', 'Ready to Invoice');
    plValueLabels.put('Review Pick up Report', 'Review Pick up Report');
    plValueLabels.put('Rework', 'Rework');
    plValueLabels.put('Request to Resend Contract', 'Request to Resend Contract');
    plValueLabels.put('Rooming List Due Date', 'Rooming List Due Date');
    plValueLabels.put('Rooming List Reminder', 'Rooming List Reminder');
    plValueLabels.put('RT Awaiting Trip Info', 'RT Awaiting Trip Info');
    plValueLabels.put('RT Confirmation Email', 'RT Confirmation Email');
    plValueLabels.put('RT FCQ', 'RT FCQ');
    plValueLabels.put('RT GCQ', 'RT GCQ');
    plValueLabels.put('Schedule Changes', 'Schedule Changes');
    plValueLabels.put('Send to Client', 'Send to Client');
    plValueLabels.put('Shuttling', 'Shuttling');
    plValueLabels.put('Tentative Dates', 'Tentative Dates');
    plValueLabels.put('Ticketed Confirmation', 'Ticketed Confirmation');
    plValueLabels.put('Travel Dates', 'Travel Dates');
    plValueLabels.put('Utilization Date', 'Utilization Date');
    plValueLabels.put('Utilization Reminder', 'Utilization Reminder');
    plValueLabels.put('Vendor Submitted Close out report', 'Vendor Submitted Close out report');

    allSubjectsSet = new Set<String>();
    for (String value : plValueLabels.keySet()) {
      if (selectOptions.size() < 1000) {
        //VFP 'Collection size maximum size of 1,000'
        selectOptions.add(new SelectOption(value, plValueLabels.get(value)));
        allSubjectsSet.add(value);
      } else
        break;
    }
    selectOptions.sort();
    //system.debug('selectOptions.size() = ' + selectOptions.size());
    searchStatusPL = selectOptions;
    //END

    searchService = new List<String>();

    //lists

    housingMapDeadlines = new Map<Id, Housing__c>();
    housingMap = new Map<Id, Housing__c>();
    bidMap_housing = new Map<Id, Bid__c>();
    lsAuditTrace_Housing = new List<Task>();
    lsJournals_Housing = new List<Journal__c>();
    lsTraces_Housing = new List<Housing__c>();
    proCoordinatorMap = new Map<String, String>();
    whatStatusToSearch = new Set<String>();

    gtMap = new Map<Id, Ground__c>();
    bidMap_GT = new Map<Id, Bid__c>();
    lsAuditTrace_GT = new List<Task>();
    lsJournals_GT = new List<Journal__c>();
    lsTraces_GT = new List<Ground__c>();

    freightMap = new Map<Id, Freight__c>();
    bidMap_Freight = new Map<Id, Bid__c>();
    lsAuditTrace_Freight = new List<Task>();
    lsJournals_Freight = new List<Journal__c>();
    lsTraces_Freight = new List<Freight__c>();

    airMap = new Map<Id, Air__c>();
    bidMap_Air = new Map<Id, Bid__c>();
    lsAuditTrace_Air = new List<Task>();
    lsJournals_Air = new List<Journal__c>();
    lsTraces_Air = new List<Air__c>();

    //airMap = new Map<Id, Air__c>();
    bidMap_AllOther = new Map<Id, Bid__c>();
    lsAuditTrace_AllOther = new List<Task>();
    lsJournals_AllOther = new List<Journal__c>();
    lsTrace_AllOther = new List<Task>();

    //tw
    lsTraceNoContract_Housing = new List<TaskWrapper>();
    lsTraceDeadlineDate_Housing = new List<TaskWrapper>();
    lsTraceNoContract_GT = new List<TaskWrapper>();
    lsTraceNoContract_Freight = new List<TaskWrapper>();
    lsTraceNoContract_Air = new List<TaskWrapper>();

    lsGroupsTWNoContract_Housing = new List<GroupTasksWrapper>();
    //lsTraceNoContract_DeadlineDate = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_GT = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_Freight = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_Air = new List<GroupTasksWrapper>();

    lsTraceContract_Housing = new List<TaskWrapper>();
    lsTraceContract_GT = new List<TaskWrapper>();
    lsTraceContract_Freight = new List<TaskWrapper>();
    lsTraceContract_Air = new List<TaskWrapper>();

    lsGroupsTW_Housing_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_GT_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_Freight_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_Air_AllOther = new List<GroupTasksWrapper>();
    sortListBy = '';
  }

  public static Map<String, String> picklistValues(String objectName, String fieldName) {
    Map<String, String> values = new Map<String, String>{};
    List<Schema.DescribeSobjectResult> results = Schema.describeSObjects(new List<String>{ objectName });

    for (Schema.DescribeSobjectResult res : results) {
      for (Schema.PicklistEntry entry : res.fields.getMap().get(fieldName).getDescribe().getPicklistValues()) {
        if (entry.isActive()) {
          values.put(entry.getValue(), entry.getLabel());
        }
      }
    }

    return values;
  }

  public void searchTrace() {
    system.debug('## TraceDashboardController - searchTrace()');

    Set<String> bidIdsWithTask = new Set<String>();

    housingMap = new Map<Id, Housing__c>();
    housingMapDeadlines = new Map<Id, Housing__c>();
    Set<String> idsWithTask_Housing = new Set<String>();
    bidMap_housing = new Map<Id, Bid__c>();
    lsAuditTrace_Housing = new List<Task>();
    lsJournals_Housing = new List<Journal__c>();
    lsTraces_Housing = new List<Housing__c>();
    proCoordinatorMap = new Map<String, String>();
    lsAuditTrace_Housing_limit = 10;
    lsJournals_Housing_limit = 10;
    loadAllContractTraces_Housing_showBtn = true;

    gtMap = new Map<Id, Ground__c>();
    Set<String> idsWithTask_GT = new Set<String>();
    bidMap_GT = new Map<Id, Bid__c>();
    lsAuditTrace_GT = new List<Task>();
    lsJournals_GT = new List<Journal__c>();
    lsTraces_GT = new List<Ground__c>();
    lsAuditTrace_GT_limit = 10;
    lsJournals_GT_limit = 10;

    freightMap = new Map<Id, Freight__c>();
    Set<String> idsWithTask_Freight = new Set<String>();
    bidMap_Freight = new Map<Id, Bid__c>();
    lsAuditTrace_Freight = new List<Task>();
    lsJournals_Freight = new List<Journal__c>();
    lsTraces_Freight = new List<Freight__c>();
    lsAuditTrace_Freight_limit = 10;
    lsJournals_Freight_limit = 10;

    airMap = new Map<Id, Air__c>();
    Set<String> idsWithTask_Air = new Set<String>();
    bidMap_Air = new Map<Id, Bid__c>();
    lsAuditTrace_Air = new List<Task>();
    lsJournals_Air = new List<Journal__c>();
    lsTraces_Air = new List<Air__c>();
    lsAuditTrace_Air_limit = 10;
    lsJournals_Air_limit = 10;

    Set<String> idsWithTask_AllOther = new Set<String>();
    bidMap_AllOther = new Map<Id, Bid__c>();
    lsAuditTrace_AllOther = new List<Task>();
    lsJournals_AllOther = new List<Journal__c>();
    lsTrace_AllOther = new List<Task>();
    lsTrace_AllOther_limit = 10;

    //tw
    lsTraceDeadlineDate_Housing = new List<TaskWrapper>();
    lsTraceNoContract_Housing = new List<TaskWrapper>();
    lsTraceNoContract_GT = new List<TaskWrapper>();
    lsTraceNoContract_Freight = new List<TaskWrapper>();
    lsTraceNoContract_Air = new List<TaskWrapper>();

    lsGroupsTWNoContract_Housing = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_GT = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_Freight = new List<GroupTasksWrapper>();
    lsGroupsTWNoContract_Air = new List<GroupTasksWrapper>();

    lsTraceContract_Housing = new List<TaskWrapper>();
    lsTraceContract_GT = new List<TaskWrapper>();
    lsTraceContract_Freight = new List<TaskWrapper>();
    lsTraceContract_Air = new List<TaskWrapper>();

    lsGroupsTW_Housing_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_GT_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_Freight_AllOther = new List<GroupTasksWrapper>();
    lsGroupsTW_Air_AllOther = new List<GroupTasksWrapper>();
    sortListBy = '';

    Set<String> bidVendorIds_housing = new Set<String>();
    Set<String> bidProductionIds_housing = new Set<String>();

    Set<String> bidVendorIds_GT = new Set<String>();
    Set<String> bidProductionIds_GT = new Set<String>();

    Set<String> bidVendorIds_Freight = new Set<String>();
    Set<String> bidProductionIds_Freight = new Set<String>();

    Set<String> bidVendorIds_Air = new Set<String>();
    Set<String> bidProductionIds_Air = new Set<String>();

    Set<String> bidVendorIds_AllOther = new Set<String>();
    Set<String> bidProductionIds_AllOther = new Set<String>();

    //COMMON - Filter by recordtypes
    Set<String> whatTypeToSearch = new Set<String>();
    Set<String> whatTypeTaskToSearch = new Set<String>();
    if (searchService.size() == 0 || searchService.contains('Housing')) {
      whatTypeToSearch.add('Housing Bid');
      whatTypeTaskToSearch.add('Housing Status Trace');
    }
    if (searchService.size() == 0 || searchService.contains('GT')) {
      whatTypeToSearch.add('GT Bid');
      whatTypeTaskToSearch.add('Ground Status Trace');
    }
    if (searchService.size() == 0 || searchService.contains('Freight')) {
      whatTypeToSearch.add('Freight Bid');
      whatTypeTaskToSearch.add('Freight Status Trace');
    }
    if (searchService.size() == 0 || searchService.contains('Air')) {
      whatTypeToSearch.add('Air Bid');
      whatTypeTaskToSearch.add('Air Status Trace');
    }

    //COMMON - proCoordinatorMap(production id, user name) used by coordinator filter
    system.debug('## searchAllCoordinators = ' + searchAllCoordinators);
    if (searchAllCoordinators)
      for (Production_Associations__c pa : [
        SELECT Id, User__c, User__r.Name, Team_Roles__c, Production_Opp__c
        FROM Production_Associations__c
        WHERE
          RecordType.Name = 'Production Coordinators'
          AND Production_Opp__c != NULL
          AND User__c != NULL
          AND Team_Roles__c INCLUDES (
            'Primary Housing Coordinator',
            'Primary GT Coordinator',
            'Primary Air Coordinator',
            'Primary Freight Coordinator'
          )
        ORDER BY User__r.Name ASC
      ])
        proCoordinatorMap.put(pa.Production_Opp__c, pa.User__r.Name);
    else
      for (Production_Associations__c pa : [
        SELECT Id, User__c, User__r.Name, Team_Roles__c, Production_Opp__c
        FROM Production_Associations__c
        WHERE
          RecordType.Name = 'Production Coordinators'
          AND Production_Opp__c != NULL
          AND User__c = :searchCoordinator
          AND Team_Roles__c INCLUDES (
            'Primary Housing Coordinator',
            'Primary GT Coordinator',
            'Primary Air Coordinator',
            'Primary Freight Coordinator'
          )
        ORDER BY User__r.Name ASC
      ])
        proCoordinatorMap.put(pa.Production_Opp__c, pa.User__r.Name);

    //COMMON - used by status filter
    system.debug('## searchAllStatus = ' + searchAllStatus);
    //Set<String> whatStatusToSearch = new Set<String>();
    whatStatusToSearch = new Set<String>();
    if (searchAllStatus)
      whatStatusToSearch = allSubjectsSet;
    else {
      for (String selectedStatus : searchStatus)
        whatStatusToSearch.add(selectedStatus);
    }

    //COMMON - used by urgent tasks only filter
    Set<String> whatPriorityToSearch = new Set<String>();
    whatPriorityToSearch.add('Urgent Follow Up');
    if (searchUrgentTaskOnly == false) {
      whatPriorityToSearch.add('Normal Follow up');
      whatPriorityToSearch.add('No Follow up');
    }

    //COMMON - bidMap(bid id, bid)
    Map<Id, Bid__c> bidMap = new Map<Id, Bid__c>();
    for (Bid__c b : [
      SELECT
        Id,
        RecordTypeId,
        RecordType.Name,
        Vendor__r.Name,
        Vendor__c,
        Contract_Due_Date__c,
        Housing__c,
        Housing__r.Date_In__c,
        Housing__r.Date_Out__c,
        Housing__r.City__r.Name,
        Housing__r.Production_CC__c,
        Housing__r.Production_CC__r.Name,
        Housing__r.Production_CC__r.Account.Name,
        Housing__r.Production_CC__r.AccountId,
        Housing__r.RecordType.Name,
        Housing__r.Trace_Date__c,
        Housing__r.Deadline_Date__c,
        GT__c,
        GT__r.Start_City__r.Name,
        GT__r.Production_Ground__c,
        GT__r.Production_Ground__r.Name,
        GT__r.Production_Ground__r.Account.Name,
        GT__r.Start_Date__c,
        GT__r.End_Date__c,
        GT__r.Description__c,
        GT__r.Service_Type_Ground__c,
        GT__r.Production_Ground__r.AccountId,
        GT__r.RecordType.Name,
        GT__r.Deadline_Date__c,
        Freight__c,
        Freight__r.Start_City__r.Name,
        Freight__r.Production__c,
        Freight__r.Production__r.Name,
        Freight__r.Production__r.Account.Name,
        Freight__r.Start_Date__c,
        Freight__r.End_Date__c,
        Freight__r.Description__c,
        Freight__r.Service_Type__c,
        Freight__r.Production__r.AccountId,
        Freight__r.RecordType.Name,
        Freight__r.Deadline_Date__c,
        Air__c,
        Air__r.Departure_Date__c,
        Air__r.Return_Date__c,
        Air__r.Arrival_Date__c,
        Air__r.Description__c,
        Air__r.Group_Type__c,
        Air__r.Trip_Type__c,
        Air__r.Production__c,
        Air__r.Production__r.Name,
        Air__r.Production__r.Account.Name,
        Air__r.Production__r.AccountId,
        Air__r.RecordType.Name,
        Air__r.Deadline_Date__c
      FROM Bid__c
      WHERE RecordType.Name = :whatTypeToSearch AND Production__c IN :proCoordinatorMap.keySet()
      ORDER BY CreatedDate DESC
      LIMIT 45000
    ])
      bidMap.put(b.Id, b);

    //LOG - result later of set values...
    system.debug('# bidMap.size() = ' + bidMap.size());
    system.debug('# searchCoordinator = ' + searchCoordinator);
    system.debug('# searchStatus = ' + searchStatus);
    system.debug('# searchService = ' + searchService);
    system.debug('# searchStartDate = ' + searchStartDate);
    system.debug('# searchEndDate = ' + searchEndDate);
    system.debug('# searchTraceType = ' + searchTraceType);
    system.debug('# whatTypeToSearch = ' + whatTypeToSearch);
    system.debug('# whatTypeTaskToSearch = ' + whatTypeTaskToSearch);
    system.debug('# proCoordinatorMap = ' + proCoordinatorMap);
    system.debug('# whatStatusToSearch = ' + whatStatusToSearch);
    system.debug('# searchUrgentTaskOnly = ' + searchUrgentTaskOnly);
    system.debug('# whatPriorityToSearch = ' + whatPriorityToSearch);

    //TRACES
    system.debug('### GET TRACES 1 (NO CONTRACTED)...');
    Set<String> tracesIdsNoContracted = new Set<String>();
    //ids services of traces (NO contracted traces)
    for (Task t : [
      SELECT
        Id,
        WhatId,
        What.type,
        Subject,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status,
        Priority
      FROM Task
      WHERE
        WhatId != NULL
        AND Task_Type__c = :whatTypeTaskToSearch
        AND RecordType.Name = 'Trace Task'
        AND ActivityDate >= :searchStartDate
        AND ActivityDate <= :searchEndDate
        AND Subject = :whatStatusToSearch
        AND Contract_Task__c = FALSE
      ORDER BY ActivityDate
    ]) {
      tracesIdsNoContracted.add(t.Id);
      if (searchTraceType == 'DeadLine Date' && t.Deadline_Date__c != null) {
        //filter 'searchTraceType'
        if (t.What.type == 'Housing__c')
          idsWithTask_Housing.add(t.WhatId);
        else if (t.What.type == 'Ground__c')
          idsWithTask_GT.add(t.WhatId);
        else if (t.What.type == 'Freight__c')
          idsWithTask_Freight.add(t.WhatId);
        else if (t.What.type == 'Air__c')
          idsWithTask_Air.add(t.WhatId);
      } else if (searchTraceType == 'Trace Date') {
        if (t.What.type == 'Housing__c')
          idsWithTask_Housing.add(t.WhatId);
        else if (t.What.type == 'Ground__c')
          idsWithTask_GT.add(t.WhatId);
        else if (t.What.type == 'Freight__c')
          idsWithTask_Freight.add(t.WhatId);
        else if (t.What.type == 'Air__c')
          idsWithTask_Air.add(t.WhatId);
      }
    }

    system.debug('# idsWithTask_Housing = ' + idsWithTask_Housing);
    system.debug('# idsWithTask_GT = ' + idsWithTask_GT);
    system.debug('# idsWithTask_Freight = ' + idsWithTask_Freight);
    system.debug('# idsWithTask_Air = ' + idsWithTask_Air);

    for (Housing__c h : [
      SELECT
        Id,
        City__r.Name,
        Status__c,
        Production_CC__c,
        Production_CC__r.Name,
        Production_CC__r.Account.Name,
        Production_CC__r.AccountId,
        Vendor_lookup__c,
        Vendor_lookup__r.Name,
        Deadline_Date__c,
        Date_In__c,
        Date_Out__c
      FROM Housing__c
      WHERE
        (Id = :idsWithTask_Housing
        AND Production_CC__c = :proCoordinatorMap.keySet()
        AND Back_End_Coordinator__c = NULL)
        OR (Back_End_Coordinator__c != NULL
        AND Trace_Date__c != NULL
        AND Back_End_Coordinator__c = :searchCoordinator)
    ]) {
      housingMap.put(h.Id, h);
    }

    for (Housing__c h : [
      SELECT
        Id,
        Status__c,
        Status_CC__c,
        CreatedBy.Name,
        City__r.Name,
        Production_CC__c,
        Production_CC__r.Name,
        Production_CC__r.Account.Name,
        Production_CC__r.AccountId,
        Vendor_lookup__c,
        Vendor_lookup__r.Name,
        Deadline_Date__c,
        Date_In__c,
        Date_Out__c
      FROM Housing__c
      WHERE
        Production_CC__c = :proCoordinatorMap.keySet()
        AND Deadline_Date__c >= :searchStartDate
        AND Deadline_Date__c <= :searchEndDate
    ]) {
      housingMapDeadlines.put(h.Id, h);
    }

    for (Ground__c g : [
      SELECT
        Id,
        Start_City__r.Name,
        Production_Ground__r.Name,
        Production_Ground__c,
        Production_Ground__r.Account.Name,
        Production_Ground__r.AccountId,
        Vendor_lookup__r.Name,
        Vendor_lookup__c,
        Deadline_Date__c,
        Start_Date__c,
        End_Date__c,
        Description__c,
        Service_Type_Ground__c
      FROM Ground__c
      WHERE Id = :idsWithTask_GT AND Production_Ground__c = :proCoordinatorMap.keySet()
    ]) {
      gtMap.put(g.Id, g);
    }

    for (Freight__c f : [
      SELECT
        Id,
        Start_City__r.Name,
        Production__r.Name,
        Production__c,
        Production__r.Account.Name,
        Production__r.AccountId,
        Vendor_lookup__r.Name,
        Vendor_lookup__c,
        Deadline_Date__c,
        Start_Date__c,
        End_Date__c,
        Description__c,
        Service_Type__c
      FROM Freight__c
      WHERE Id = :idsWithTask_Freight AND Production__c = :proCoordinatorMap.keySet()
    ]) {
      freightMap.put(f.Id, f);
    }

    for (Air__c a : [
      SELECT
        Id,
        Production__r.Name,
        Production__c,
        Production__r.Account.Name,
        Production__r.AccountId,
        Vendor__r.Name,
        Vendor__c,
        Deadline_Date__c,
        Departure_Date__c,
        Return_Date__c,
        Description__c,
        Group_Type__c,
        Trip_Type__c
      FROM Air__c
      WHERE Id = :idsWithTask_Air AND Production__c = :proCoordinatorMap.keySet()
    ]) {
      airMap.put(a.Id, a);
    }

    system.debug('# housingMap = ' + housingMap);
    system.debug('# gtMap = ' + gtMap);
    system.debug('# freightMap = ' + freightMap);
    system.debug('# airMap = ' + airMap);

    for (Housing__c h : housingMapDeadlines.values()) {
      if (h.Deadline_Date__c >= searchStartDate && h.Deadline_Date__c <= searchEndDate) {
        lsTraceDeadlineDate_Housing.add(
          new TaskWrapper(
            h.id,
            null,
            h.Id,
            'High',
            h.Deadline_Date__c,
            h.City__r.Name,
            h.Production_CC__r.Name,
            h.Production_CC__c,
            h.Production_CC__r.Account.Name,
            h.Production_CC__r.AccountId,
            h.Vendor_lookup__r.Name,
            h.Vendor_lookup__c,
            'Deadline Date',
            h.Production_CC__c,
            h.Deadline_Date__c,
            h.Date_In__c,
            h.Date_Out__c,
            null,
            null,
            null,
            null,
            null,
            null,
            '',
            '',
            ''
          )
        );
      }
    }

    Map<String, TaskWrapper> theTraceTasks = new Map<String, TaskWrapper>();

    //set traces..
    for (Task t : [
      SELECT
        Id,
        WhatId,
        What.type,
        Subject,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status,
        Priority
      FROM Task
      WHERE
        (WhatId = :housingMap.keySet()
        OR WhatId = :gtMap.keySet()
        OR WhatId = :freightMap.keySet()
        OR WhatId = :airMap.keySet())
        AND Id = :tracesIdsNoContracted
      ORDER BY ActivityDate
    ]) {
      //FROM Task WHERE WhatId <> NULL AND Task_Type__c =: whatTypeTaskToSearch AND RecordType.Name = 'Trace Task' AND ActivityDate >= :searchStartDate AND ActivityDate <= :searchEndDate AND Subject =: whatStatusToSearch AND Contract_Task__c = false ORDER BY ActivityDate]){
      system.debug('# t = ' + t);

      if (housingMap.get(t.WhatId) != null) {
        system.debug('# Housing id = ' + t.WhatId);
        system.debug('# t.id = ' + t.id);
        theTraceTasks.put(
          t.whatId,
          new TaskWrapper(
            t.id,
            null,
            t.WhatId,
            t.Priority,
            t.ActivityDate,
            housingMap.get(t.WhatId).City__r.Name,
            housingMap.get(t.WhatId).Production_CC__r.Name,
            housingMap.get(t.WhatId).Production_CC__c,
            housingMap.get(t.WhatId).Production_CC__r.Account.Name,
            housingMap.get(t.WhatId).Production_CC__r.AccountId,
            housingMap.get(t.WhatId).Vendor_lookup__r.Name,
            housingMap.get(t.WhatId).Vendor_lookup__c,
            t.Subject,
            proCoordinatorMap.get(housingMap.get(t.WhatId).Production_CC__c),
            housingMap.get(t.WhatId).Deadline_Date__c,
            housingMap.get(t.WhatId).Date_In__c,
            housingMap.get(t.WhatId).Date_Out__c,
            null,
            null,
            null,
            null,
            null,
            null,
            '',
            '',
            ''
          )
        );
      } else if (gtMap.get(t.WhatId) != null) {
        system.debug('# GT id = ' + t.WhatId);
        system.debug('# t.id = ' + t.id);

        lsTraceNoContract_GT.add(
          new TaskWrapper(
            t.id,
            null,
            t.WhatId,
            t.Priority,
            t.ActivityDate,
            gtMap.get(t.WhatId).Start_City__r.Name,
            gtMap.get(t.WhatId).Production_Ground__r.Name,
            gtMap.get(t.WhatId).Production_Ground__c,
            gtMap.get(t.WhatId).Production_Ground__r.Account.Name,
            gtMap.get(t.WhatId).Production_Ground__r.AccountId,
            gtMap.get(t.WhatId).Vendor_lookup__r.Name,
            gtMap.get(t.WhatId).Vendor_lookup__c,
            t.Subject,
            proCoordinatorMap.get(gtMap.get(t.WhatId).Production_Ground__c),
            gtMap.get(t.WhatId).Deadline_Date__c,
            null,
            null,
            gtMap.get(t.WhatId).Start_Date__c,
            gtMap.get(t.WhatId).End_Date__c,
            gtMap.get(t.WhatId).Description__c,
            gtMap.get(t.WhatId).Service_Type_Ground__c,
            null,
            null,
            '',
            '',
            ''
          )
        );
      } else if (freightMap.get(t.WhatId) != null) {
        system.debug('# Freight id = ' + t.WhatId);
        system.debug('# t.id = ' + t.id);

        lsTraceNoContract_Freight.add(
          new TaskWrapper(
            t.id,
            null,
            t.WhatId,
            t.Priority,
            t.ActivityDate,
            freightMap.get(t.WhatId).Start_City__r.Name,
            freightMap.get(t.WhatId).Production__r.Name,
            freightMap.get(t.WhatId).Production__c,
            freightMap.get(t.WhatId).Production__r.Account.Name,
            freightMap.get(t.WhatId).Production__r.AccountId,
            freightMap.get(t.WhatId).Vendor_lookup__r.Name,
            freightMap.get(t.WhatId).Vendor_lookup__c,
            t.Subject,
            proCoordinatorMap.get(freightMap.get(t.WhatId).Production__c),
            freightMap.get(t.WhatId).Deadline_Date__c,
            null,
            null,
            freightMap.get(t.WhatId).Start_Date__c,
            freightMap.get(t.WhatId).End_Date__c,
            freightMap.get(t.WhatId).Description__c,
            freightMap.get(t.WhatId).Service_Type__c,
            null,
            null,
            '',
            '',
            ''
          )
        );
      } else if (airMap.get(t.WhatId) != null) {
        system.debug('# Air id = ' + t.WhatId);
        system.debug('# t.id = ' + t.id);

        lsTraceNoContract_Air.add(
          new TaskWrapper(
            t.id,
            null,
            t.WhatId,
            t.Priority,
            t.ActivityDate,
            null,
            airMap.get(t.WhatId).Production__r.Name,
            airMap.get(t.WhatId).Production__c,
            airMap.get(t.WhatId).Production__r.Account.Name,
            airMap.get(t.WhatId).Production__r.AccountId,
            airMap.get(t.WhatId).Vendor__r.Name,
            airMap.get(t.WhatId).Vendor__c,
            t.Subject,
            proCoordinatorMap.get(airMap.get(t.WhatId).Production__c),
            airMap.get(t.WhatId).Deadline_Date__c,
            null,
            null,
            null,
            null,
            null,
            null,
            airMap.get(t.WhatId).Departure_Date__c,
            //bidMap.get(t.WhatId).Air__r.Arrival_Date__c,
            airMap.get(t.WhatId).Return_Date__c,
            airMap.get(t.WhatId).Description__c,
            airMap.get(t.WhatId).Group_Type__c,
            airMap.get(t.WhatId).Trip_Type__c
          )
        );
      }
    }

    lsTraceNoContract_Housing = theTraceTasks.values();
    //END GET TRACES 1

    system.debug('### GET TRACES 2 (CONTRACTED)...');
    for (Task t : [
      SELECT
        Id,
        WhatId,
        What.type,
        Subject,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status,
        Priority
      FROM Task
      WHERE
        WhatId IN (
          SELECT id
          FROM Bid__c
          WHERE
            RecordType.Name = :whatTypeToSearch
            AND Status__c IN ('Contracted', 'In Contracting', 'Pending Client Signature')
        )
        AND Contract_Task__c = TRUE
        AND RecordType.Name = 'Trace Task'
        AND ActivityDate >= :searchStartDate
        AND ActivityDate <= :searchEndDate
        AND Subject = :whatStatusToSearch
        AND Priority = :whatPriorityToSearch
        AND Subject != 'Pending Client Choice'
      ORDER BY ActivityDate
    ]) {
      system.debug('# t = ' + t);
      if (bidMap.get(t.WhatId) != null) {
        //according...
        if (
          bidMap.get(t.WhatId).RecordType.Name == 'Housing Bid' &&
          proCoordinatorMap.containsKey(bidMap.get(t.WhatId).Housing__r.Production_CC__c) &&
          bidMap.get(t.WhatId).Contract_Due_Date__c != null
        ) {
          system.debug('# Housing Bid id = ' + t.WhatId);
          system.debug('# t.id = ' + t.id);

          lsTraceContract_Housing.add(
            new TaskWrapper(
              /*((t.Status.equals('Completed'))? true : false),*/
              t.id,
              t.WhatId,
              null,
              t.Priority,
              t.ActivityDate,
              bidMap.get(t.WhatId).Housing__r.City__r.Name,
              bidMap.get(t.WhatId).Housing__r.Production_CC__r.Name,
              bidMap.get(t.WhatId).Housing__r.Production_CC__c,
              bidMap.get(t.WhatId).Housing__r.Production_CC__r.Account.Name,
              bidMap.get(t.WhatId).Housing__r.Production_CC__r.AccountId,
              bidMap.get(t.WhatId).Vendor__r.Name,
              bidMap.get(t.WhatId).Vendor__c,
              t.Subject,
              proCoordinatorMap.get(bidMap.get(t.WhatId).Housing__r.Production_CC__c),
              null,
              bidMap.get(t.WhatId).Housing__r.Date_In__c,
              bidMap.get(t.WhatId).Housing__r.Date_Out__c,
              null,
              null,
              null,
              null,
              null,
              null,
              '',
              '',
              ''
            )
          );
        } else if (
          bidMap.get(t.WhatId).RecordType.Name == 'GT Bid' &&
          proCoordinatorMap.containsKey(bidMap.get(t.WhatId).GT__r.Production_Ground__c)
        ) {
          system.debug('# GT Bid id = ' + t.WhatId);
          system.debug('# t.id = ' + t.id);

          lsTraceContract_GT.add(
            new TaskWrapper(
              t.id,
              t.WhatId,
              null,
              t.Priority,
              t.ActivityDate,
              bidMap.get(t.WhatId).GT__r.Start_City__r.Name,
              bidMap.get(t.WhatId).GT__r.Production_Ground__r.Name,
              bidMap.get(t.WhatId).GT__r.Production_Ground__c,
              bidMap.get(t.WhatId).GT__r.Production_Ground__r.Account.Name,
              bidMap.get(t.WhatId).GT__r.Production_Ground__r.AccountId,
              bidMap.get(t.WhatId).Vendor__r.Name,
              bidMap.get(t.WhatId).Vendor__c,
              t.Subject,
              proCoordinatorMap.get(bidMap.get(t.WhatId).GT__r.Production_Ground__c),
              null,
              null,
              null,
              bidMap.get(t.WhatId).GT__r.Start_Date__c,
              bidMap.get(t.WhatId).GT__r.End_Date__c,
              bidMap.get(t.WhatId).GT__r.Description__c,
              bidMap.get(t.WhatId).GT__r.Service_Type_Ground__c,
              null,
              null,
              '',
              '',
              ''
            )
          );
        } else if (
          bidMap.get(t.WhatId).RecordType.Name == 'Freight Bid' &&
          proCoordinatorMap.containsKey(bidMap.get(t.WhatId).Freight__r.Production__c)
        ) {
          system.debug('# Freight Bid id = ' + t.WhatId);
          system.debug('# t.id = ' + t.id);

          lsTraceContract_Freight.add(
            new TaskWrapper(
              t.id,
              t.WhatId,
              null,
              t.Priority,
              t.ActivityDate,
              bidMap.get(t.WhatId).Freight__r.Start_City__r.Name,
              bidMap.get(t.WhatId).Freight__r.Production__r.Name,
              bidMap.get(t.WhatId).Freight__r.Production__c,
              bidMap.get(t.WhatId).Freight__r.Production__r.Account.Name,
              bidMap.get(t.WhatId).Freight__r.Production__r.AccountId,
              bidMap.get(t.WhatId).Vendor__r.Name,
              bidMap.get(t.WhatId).Vendor__c,
              t.Subject,
              proCoordinatorMap.get(bidMap.get(t.WhatId).Freight__r.Production__c),
              null,
              null,
              null,
              bidMap.get(t.WhatId).Freight__r.Start_Date__c,
              bidMap.get(t.WhatId).Freight__r.End_Date__c,
              bidMap.get(t.WhatId).Freight__r.Description__c,
              bidMap.get(t.WhatId).Freight__r.Service_Type__c,
              null,
              null,
              '',
              '',
              ''
            )
          );
        } else if (
          bidMap.get(t.WhatId).RecordType.Name == 'Air Bid' &&
          proCoordinatorMap.containsKey(bidMap.get(t.WhatId).Air__r.Production__c)
        ) {
          system.debug('# Air Bid id = ' + t.WhatId);
          system.debug('# t.id = ' + t.id);

          lsTraceContract_Air.add(
            new TaskWrapper(
              t.id,
              t.WhatId,
              null,
              t.Priority,
              t.ActivityDate,
              null,
              bidMap.get(t.WhatId).Air__r.Production__r.Name,
              bidMap.get(t.WhatId).Air__r.Production__c,
              bidMap.get(t.WhatId).Air__r.Production__r.Account.Name,
              bidMap.get(t.WhatId).Air__r.Production__r.AccountId,
              bidMap.get(t.WhatId).Vendor__r.Name,
              bidMap.get(t.WhatId).Vendor__c,
              t.Subject,
              proCoordinatorMap.get(bidMap.get(t.WhatId).Air__r.Production__c),
              null,
              null,
              null,
              null,
              null,
              null,
              null,
              bidMap.get(t.WhatId).Air__r.Departure_Date__c,
              //bidMap.get(t.WhatId).Air__r.Arrival_Date__c,
              bidMap.get(t.WhatId).Air__r.Return_Date__c,
              bidMap.get(t.WhatId).Air__r.Description__c,
              bidMap.get(t.WhatId).Air__r.Group_Type__c,
              bidMap.get(t.WhatId).Air__r.Trip_Type__c
            )
          );
        }
      }
    }
    //END GET TRACES 2

    /** HOUSING **/
    if (searchService.size() == 0 || searchService.contains('Housing')) {
      //AUDITS
      loadAuditTrace_Housing();

      loadJournals_Housing();

      if (lsTraceNoContract_Housing.size() > 0) {
        system.debug('## lsTraceNoContract_Housing.size() = ' + lsTraceNoContract_Housing.size());

        //sort list..
        lsTraceNoContract_Housing.sort();

        //call to groupmethod..
        lsGroupsTWNoContract_Housing = groupListByField(lsTraceNoContract_Housing, searchSortBy);
        system.debug('## lsGroupsTWNoContract_Housing.size() = ' + lsGroupsTWNoContract_Housing.size());

        //limit each sublist to 10
        for (GroupTasksWrapper gtw : lsGroupsTWNoContract_Housing)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }

      //TRACES 2
      if (lsTraceContract_Housing.size() > 0) {
        system.debug('## lsTraceContract_Housing.size() = ' + lsTraceContract_Housing.size());
        lsTraceContract_Housing.sort();
        lsGroupsTW_Housing_AllOther = groupListByField(lsTraceContract_Housing, searchSortBy);
        system.debug('## lsGroupsTW_Housing_AllOther.size() = ' + lsGroupsTW_Housing_AllOther.size());
        for (GroupTasksWrapper gtw : lsGroupsTW_Housing_AllOther)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }
    }

    /** GROUND **/
    if (searchService.size() == 0 || searchService.contains('GT')) {
      //AUDITS
      loadAuditTrace_GT();
      loadJournals_GT();
      if (lsTraceNoContract_GT.size() > 0) {
        system.debug('## lsTraceNoContract_GT.size() = ' + lsTraceNoContract_GT.size());

        lsTraceNoContract_GT.sort();

        lsGroupsTWNoContract_GT = groupListByField(lsTraceNoContract_GT, searchSortBy);
        system.debug('## lsGroupsTWNoContract_GT.size() = ' + lsGroupsTWNoContract_GT.size());

        for (GroupTasksWrapper gtw : lsGroupsTWNoContract_GT)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }

      if (lsTraceContract_GT.size() > 0) {
        system.debug('## lsTraceContract_GT.size() = ' + lsTraceContract_GT.size());

        //sort list..
        lsTraceContract_GT.sort();

        //call to groupmethod..
        lsGroupsTW_GT_AllOther = groupListByField(lsTraceContract_GT, searchSortBy);
        system.debug('## lsGroupsTW_GT_AllOther.size() = ' + lsGroupsTW_GT_AllOther.size());

        //TEST 220120
        for (GroupTasksWrapper gtw : lsGroupsTW_GT_AllOther)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }
    }

    /** FREIGHT **/
    if (searchService.size() == 0 || searchService.contains('Freight')) {
      //AUDITS
      loadAuditTrace_Freight();

      loadAllJournals_Freight();

      if (lsTraceNoContract_Freight.size() > 0) {
        system.debug('## lsTraceNoContract_Freight.size() = ' + lsTraceNoContract_Freight.size());

        //sort list..
        lsTraceNoContract_Freight.sort();

        //call to groupmethod..
        lsGroupsTWNoContract_Freight = groupListByField(lsTraceNoContract_Freight, searchSortBy);
        system.debug('## lsGroupsTWNoContract_Freight.size() = ' + lsGroupsTWNoContract_Freight.size());

        //limit each sublist to 10
        for (GroupTasksWrapper gtw : lsGroupsTWNoContract_Freight)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }

      //TRACES 2
      if (lsTraceContract_Freight.size() > 0) {
        system.debug('## lsTraceContract_Freight.size() = ' + lsTraceContract_Freight.size());

        //sort list..
        lsTraceContract_Freight.sort();

        //call to groupmethod..
        lsGroupsTW_Freight_AllOther = groupListByField(lsTraceContract_Freight, searchSortBy);
        system.debug('## lsGroupsTW_Freight_AllOther.size() = ' + lsGroupsTW_Freight_AllOther.size());

        //TEST 220120
        for (GroupTasksWrapper gtw : lsGroupsTW_Freight_AllOther)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }
    }

    /** AIR **/
    if (searchService.size() == 0 || searchService.contains('Air')) {
      loadAuditTrace_Air();
      loadJournals_Air();

      if (lsTraceNoContract_Air.size() > 0) {
        system.debug('## lsTraceNoContract_Air.size() = ' + lsTraceNoContract_Air.size());

        //sort list..
        lsTraceNoContract_Air.sort();

        //call to groupmethod..
        lsGroupsTWNoContract_Air = groupListByField(lsTraceNoContract_Air, searchSortBy);
        system.debug('## lsGroupsTWNoContract_Air.size() = ' + lsGroupsTWNoContract_Air.size());

        //limit each sublist to 10
        for (GroupTasksWrapper gtw : lsGroupsTWNoContract_Air)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }

      //TRACES 2
      if (lsTraceContract_Air.size() > 0) {
        system.debug('## lsTraceContract_Air.size() = ' + lsTraceContract_Air.size());

        //sort list..
        lsTraceContract_Air.sort();

        //call to groupmethod..
        lsGroupsTW_Air_AllOther = groupListByField(lsTraceContract_Air, searchSortBy);
        system.debug('## lsGroupsTW_Air_AllOther.size() = ' + lsGroupsTW_Air_AllOther.size());

        //TEST 220120
        for (GroupTasksWrapper gtw : lsGroupsTW_Air_AllOther)
          gtw.lsTasks = selectRowsListPagination(gtw.lsTasks, 10);
      }
    }

    /** ALL OTHER **/
    if (whatTypeToSearch.size() > 0) {
      loadTrace_AllOther();
    }
  }

  //HOUSING
  public void loadAllAuditTrace_Housing() {
    system.debug('## loadAllAuditTrace_Housing()');
    lsAuditTrace_Housing_limit = 1000;
    loadAuditTrace_Housing();
  }

  public void loadAuditTrace_Housing() {
    system.debug('## loadAuditTrace_Housing()');
    system.debug('## lsAuditTrace_Housing_limit = ' + lsAuditTrace_Housing_limit);

    lsAuditTrace_Housing = new List<Task>();
    Set<String> idsWithTask_HousingAux = new Set<String>();
    housingMap = new Map<Id, Housing__c>();

    for (Task t : [
      SELECT
        Id,
        Subject,
        WhatId,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status
      FROM Task
      WHERE
        WhatId != NULL
        AND What.type = 'Housing__c'
        AND RecordType.Name = 'Trace Task' /*AND ActivityDate >= :searchStartDate AND ActivityDate <= :searchEndDate*/
        AND IsForAudit__c = TRUE
        AND (CreatedBy.Name = :proCoordinatorMap.values()
        OR Owner.Name = :proCoordinatorMap.values())
        AND Status != 'Completed'
      ORDER BY createddate
      LIMIT :lsAuditTrace_Housing_limit
    ]) {
      lsAuditTrace_Housing.add(t);
      idsWithTask_HousingAux.add(t.WhatId);
    }
    system.debug('## lsAuditTrace_Housing.size() = ' + lsAuditTrace_Housing.size());

    //aux map
    for (Housing__c h : [
      SELECT
        Id,
        Production_CC__c,
        Production_CC__r.Name,
        City__r.Name,
        Production_CC__r.AccountId,
        Production_CC__r.Account.Name
      FROM Housing__c
      WHERE Id = :idsWithTask_HousingAux
    ])
      housingMap.put(h.id, h);
  }

  public void loadAllJournals_Housing() {
    system.debug('## loadAllJournals_Housing()');
    lsJournals_Housing_limit = 1000;
    loadJournals_Housing();
  }

  public void loadJournals_Housing() {
    lsJournals_Housing = [
      SELECT
        Id,
        Trace_Date__c,
        Journal_Entry__c,
        CreatedById,
        CreatedBy.Name,
        CreatedDate,
        Trace_Coordinator__c,
        Trace_Coordinator__r.Name,
        Bid__c,
        Bid__r.Name,
        Bid__r.Stay_ID__c,
        Bid__r.Contract_ID__c,
        Production__r.Name,
        (SELECT Name, Contact__r.Name FROM Related_Contact__r),
        (SELECT Name, Company__r.Name FROM Related_Companies__r)
      FROM Journal__c
      WHERE
        Housing__c != NULL /*Housing__c =: idsWithTask_Housing*/
        AND Trace_Date__c >= :searchStartDate
        AND Trace_Date__c <= :searchEndDate
        AND Trace_Coordinator__r.Name = :proCoordinatorMap.values()
        AND Mark_Journal_trace_complete__c = FALSE
      /*Trace_Coordinator__c <> NULL AND (RecordType.Name = 'Bid Journal' OR RecordType.Name = 'Trip Journal') ORDER BY createddate*/ LIMIT :lsJournals_Housing_limit
    ];
    system.debug('## lsJournals_Housing.size() = ' + lsJournals_Housing.size());
  }

  public void loadAllTraces_Housing() {
    system.debug('## loadAllTraces_Housing()');
    lsGroupsTWNoContract_Housing = groupListByField(lsTraceNoContract_Housing, searchSortBy);
    system.debug('## lsGroupsTWNoContract_Housing.size() = ' + lsGroupsTWNoContract_Housing.size());
  }

  public void loadAllContractTraces_Housing() {
    system.debug('## loadAllContractTraces_Housing()');
    loadAllContractTraces_Housing_showBtn = false;
    lsGroupsTW_Housing_AllOther = groupListByField(lsTraceContract_Housing, searchSortBy);
    system.debug('## lsGroupsTW_Housing_AllOther.size() = ' + lsGroupsTW_Housing_AllOther.size());
  }
  //END

  //GT
  public void loadAllAuditTrace_GT() {
    system.debug('## loadAllAuditTrace_GT()');
    lsAuditTrace_Housing_limit = 1000;
    loadAuditTrace_GT();
  }

  public void loadAuditTrace_GT() {
    system.debug('## loadAuditTrace_GT()');
    system.debug('## lsAuditTrace_GT_limit = ' + lsAuditTrace_GT_limit);

    lsAuditTrace_GT = new List<Task>();
    Set<String> idsWithTask_GT = new Set<String>();
    gtMap = new Map<Id, Ground__c>();

    for (Task t : [
      SELECT
        Id,
        Subject,
        WhatId,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status
      FROM Task
      WHERE
        WhatId != NULL
        AND What.type = 'Ground__c'
        AND (CreatedBy.Name = :proCoordinatorMap.values()
        OR Owner.Name = :proCoordinatorMap.values())
        AND RecordType.Name = 'Trace Task'
      ORDER BY createddate
      LIMIT :lsAuditTrace_GT_limit
    ]) {
      lsAuditTrace_GT.add(t);
      idsWithTask_GT.add(t.WhatId);
    }

    //aux map
    for (Ground__c g : [
      SELECT
        Id,
        Production_Ground__c,
        Production_Ground__r.Name,
        Start_City__r.Name,
        Production_Ground__r.AccountId,
        Production_Ground__r.Account.Name
      FROM Ground__c
      WHERE Id = :idsWithTask_GT
    ])
      gtMap.put(g.id, g);
  }

  public void loadAllJournals_GT() {
    system.debug('## loadAllJournals_GT()');
    lsJournals_GT_limit = 1000;
    loadJournals_GT();
  }

  public void loadJournals_GT() {
    lsJournals_GT = [
      SELECT
        Id,
        Trace_Date__c,
        Journal_Entry__c,
        CreatedById,
        CreatedBy.Name,
        CreatedDate,
        Trace_Coordinator__c,
        Trace_Coordinator__r.Name,
        Bid__c,
        Bid__r.Name,
        Bid__r.Stay_ID__c,
        Bid__r.Contract_ID__c,
        Production__r.Name,
        (SELECT Name, Contact__r.Name FROM Related_Contact__r),
        (SELECT Name, Company__r.Name FROM Related_Companies__r)
      FROM Journal__c
      WHERE
        G__c != NULL
        AND Trace_Date__c >= :searchStartDate
        AND Trace_Date__c <= :searchEndDate
        AND Trace_Coordinator__r.Name = :proCoordinatorMap.values()
        AND Mark_Journal_trace_complete__c = FALSE
      LIMIT :lsJournals_GT_limit
    ];
    system.debug('## lsJournals_GT.size() = ' + lsJournals_GT.size());
  }
  //END

  //FREIGHT
  public void loadAllAuditTrace_Freight() {
    system.debug('## loadAllAuditTrace_Freight()');
    lsAuditTrace_Freight_limit = 1000;
    loadAuditTrace_Freight();
  }

  public void loadAuditTrace_Freight() {
    system.debug('## loadAuditTrace_Freight()');
    system.debug('## lsAuditTrace_Freight_limit = ' + lsAuditTrace_Freight_limit);

    lsAuditTrace_Freight = new List<Task>();
    Set<String> idsWithTask_Freight = new Set<String>();
    freightMap = new Map<Id, Freight__c>();

    for (Task t : [
      SELECT
        Id,
        Subject,
        WhatId,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status
      FROM Task
      WHERE
        WhatId != NULL
        AND What.type = 'Freight__c'
        AND (CreatedBy.Name = :proCoordinatorMap.values()
        OR Owner.Name = :proCoordinatorMap.values())
        AND RecordType.Name = 'Trace Task'
      ORDER BY createddate
      LIMIT :lsAuditTrace_Freight_limit
    ]) {
      lsAuditTrace_Freight.add(t);
      idsWithTask_Freight.add(t.WhatId);
    }

    //aux map
    for (Freight__c f : [
      SELECT
        Id,
        Production__c,
        Production__r.Name,
        Start_City__r.Name,
        Production__r.AccountId,
        Production__r.Account.Name
      FROM Freight__c
      WHERE Id = :idsWithTask_Freight
    ])
      freightMap.put(f.id, f);
  }

  public void loadAllJournals_Freight() {
    system.debug('## loadAllJournals_Freight()');
    lsJournals_Freight_limit = 1000;
    loadJournals_Freight();
  }

  public void loadJournals_Freight() {
    lsJournals_Freight = [
      SELECT
        Id,
        Trace_Date__c,
        Journal_Entry__c,
        CreatedById,
        CreatedBy.Name,
        CreatedDate,
        Trace_Coordinator__c,
        Trace_Coordinator__r.Name,
        Bid__c,
        Bid__r.Name,
        Bid__r.Stay_ID__c,
        Bid__r.Contract_ID__c,
        Production__r.Name,
        (SELECT Name, Contact__r.Name FROM Related_Contact__r),
        (SELECT Name, Company__r.Name FROM Related_Companies__r)
      FROM Journal__c
      WHERE
        Freight__c != NULL
        AND Trace_Date__c >= :searchStartDate
        AND Trace_Date__c <= :searchEndDate
        AND Trace_Coordinator__r.Name = :proCoordinatorMap.values()
        AND Mark_Journal_trace_complete__c = FALSE
      LIMIT :lsJournals_Freight_limit
    ];
    system.debug('## lsJournals_Freight.size() = ' + lsJournals_Freight.size());
  }
  //END

  //AIR
  public void loadAllAuditTrace_Air() {
    system.debug('## loadAllAuditTrace_Air()');
    lsAuditTrace_Air_limit = 1000;
    loadAuditTrace_Air();
  }
  public void loadAuditTrace_Air() {
    system.debug('## loadAuditTrace_Air()');
    system.debug('## lsAuditTrace_Air_limit = ' + lsAuditTrace_Air_limit);

    lsAuditTrace_Air = new List<Task>();
    Set<String> idsWithTask_Air = new Set<String>();
    airMap = new Map<Id, Air__c>();

    for (Task t : [
      SELECT
        Id,
        Subject,
        WhatId,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status
      FROM Task
      WHERE
        WhatId != NULL
        AND What.type = 'Air__c'
        AND (CreatedBy.Name = :proCoordinatorMap.values()
        OR Owner.Name = :proCoordinatorMap.values())
        AND RecordType.Name = 'Trace Task'
      ORDER BY createddate
      LIMIT :lsAuditTrace_Air_limit
    ]) {
      lsAuditTrace_Air.add(t);
      idsWithTask_Air.add(t.WhatId);
    }

    //aux map
    for (Air__c a : [
      SELECT
        Id,
        Production__c,
        Production__r.Name,
        Departure_City__r.Name,
        Production__r.AccountId,
        Production__r.Account.Name
      FROM Air__c
      WHERE Id = :idsWithTask_Air
    ])
      airMap.put(a.id, a);
  }

  public void loadAllJournals_Air() {
    system.debug('## loadAllJournals_Air()');
    lsJournals_Air_limit = 1000;
    loadJournals_Air();
  }

  public void loadJournals_Air() {
    lsJournals_Air = [
      SELECT
        Id,
        Trace_Date__c,
        Journal_Entry__c,
        CreatedById,
        CreatedBy.Name,
        CreatedDate,
        Trace_Coordinator__c,
        Trace_Coordinator__r.Name,
        Bid__c,
        Bid__r.Name,
        Bid__r.Stay_ID__c,
        Bid__r.Contract_ID__c,
        Production__r.Name,
        (SELECT Name, Contact__r.Name FROM Related_Contact__r),
        (SELECT Name, Company__r.Name FROM Related_Companies__r)
      FROM Journal__c
      WHERE
        Air__c != NULL
        AND Trace_Date__c >= :searchStartDate
        AND Trace_Date__c <= :searchEndDate
        AND Trace_Coordinator__r.Name = :proCoordinatorMap.values()
        AND Mark_Journal_trace_complete__c = FALSE
      LIMIT :lsJournals_Air_limit
    ];
    system.debug('## lsJournals_Air.size() = ' + lsJournals_Air.size());
  }

  public void loadAllTraces_Air() {
    system.debug('## loadAllTraces_Air()');
    lsGroupsTWNoContract_Air = groupListByField(lsTraceNoContract_Air, searchSortBy);
    system.debug('## lsGroupsTWNoContract_Air.size() = ' + lsGroupsTWNoContract_Air.size());
  }

  public void loadAllContractTraces_Air() {
    system.debug('## loadAllContractTraces_Air()');
    //loadAllContractTraces_Air_showBtn = false;
    lsGroupsTW_Air_AllOther = groupListByField(lsTraceContract_Air, searchSortBy);
    system.debug('## lsGroupsTW_Air_AllOther.size() = ' + lsGroupsTW_Air_AllOther.size());
  }
  //END

  //ALL OTHER TRACES
  public void loadAllTrace_AllOther() {
    system.debug('## loadAllTrace_AllOthe()');
    lsTrace_AllOther_limit = 1000;
    loadTrace_AllOther();
  }

  public void loadTrace_AllOther() {
    system.debug('## loadTrace_AllOther()');
    system.debug('## lsTrace_AllOther_limit = ' + lsTrace_AllOther_limit);

    lsTrace_AllOther = new List<Task>();

    for (Task t : [
      SELECT
        Id,
        Service_Id__c,
        Subject,
        WhatId,
        Deadline_Date__c,
        ActivityDate,
        CreatedById,
        CreatedBy.Name,
        OwnerId,
        Owner.Name,
        Status,
        IsForCloseOut__c
      FROM Task
      WHERE
        WhatId != NULL
        AND (What.type != 'Bid__c'
        OR (What.type = 'Bid__c'
        AND IsForCloseOut__c = TRUE))
        AND What.type != 'Housing__c'
        AND What.type != 'Ground__c'
        AND What.type != 'Freight__c'
        AND What.type != 'Air__c'
        AND Subject = :whatStatusToSearch
        AND RecordType.Name = 'Trace Task'
        AND (CreatedBy.Name = :proCoordinatorMap.values()
        OR Owner.Name = :proCoordinatorMap.values())
        AND ActivityDate >= :searchStartDate
        AND ActivityDate <= :searchEndDate
        AND Status != 'Completed'
      ORDER BY createddate
      LIMIT :lsTrace_AllOther_limit
    ]) {
      //lsTrace_AllOther.add(t);
      if (searchTraceType == 'DeadLine Date' && t.Deadline_Date__c != null) {
        //filter 'searchTraceType'
        lsTrace_AllOther.add(t);
      } else if (searchTraceType == 'Trace Date') {
        lsTrace_AllOther.add(t);
      }
    }
    system.debug('## lsTrace_AllOther.size() = ' + lsTrace_AllOther.size());
  }
  //END

  public static List<GroupTasksWrapper> groupListByField(List<TaskWrapper> listTW, String groupBy_searchSortBy) {
    system.debug('## groupListByField()');
    Set<String> auxSetString = new Set<String>();
    Set<Date> auxSetDate = new Set<Date>();
    List<TaskWrapper> auxlsTW;
    Integer count;
    List<GroupTasksWrapper> lsGroup = new List<GroupTasksWrapper>();

    //add all values of the field by groupBy_searchSortBy, to map (auxSet..)
    for (TaskWrapper tw : listTW) {
      //according...
      if (groupBy_searchSortBy == 'By Status')
        auxSetString.add(tw.status);
      else if (groupBy_searchSortBy == 'By Production')
        auxSetString.add(tw.production);
      else if (groupBy_searchSortBy == 'By Company')
        auxSetString.add(tw.companies);
      else if (groupBy_searchSortBy == 'By City')
        auxSetString.add(tw.city);
      else if (groupBy_searchSortBy == 'By Date')
        auxSetDate.add(tw.followUpDate);
      else if (groupBy_searchSortBy == 'By Coordinator')
        auxSetString.add(tw.coordinator);
      else if (groupBy_searchSortBy == 'By Vendor')
        auxSetString.add(tw.vendor);
    }

    //search and compare each value in map (auxSet..) with the list (listTW)
    //only if is STRING the value to group
    if (auxSetString.size() > 0)
      for (String currentVal : auxSetString) {
        auxlsTW = new List<TaskWrapper>();
        count = 0;

        //grouping.. to aux list
        for (TaskWrapper tw : listTW) {
          //according...
          if (
            (groupBy_searchSortBy == 'By Status' &&
            tw.status == currentVal) ||
            (groupBy_searchSortBy == 'By Production' &&
            tw.production == currentVal) ||
            (groupBy_searchSortBy == 'By Company' &&
            tw.companies == currentVal) ||
            (groupBy_searchSortBy == 'By City' &&
            tw.city == currentVal) ||
            (groupBy_searchSortBy == 'By Coordinator' &&
            tw.coordinator == currentVal) ||
            (groupBy_searchSortBy == 'By Vendor' &&
            tw.vendor == currentVal)
          ) {
            auxlsTW.add(tw);
            count++;
          }
        }

        //add aux list to new group
        if (auxlsTW.size() > 0)
          lsGroup.add(new GroupTasksWrapper(currentVal, auxlsTW, count));
      }
    else if (auxSetDate.size() > 0)
      //only if is DATE the value to group
      for (Date currentVal : auxSetDate) {
        auxlsTW = new List<TaskWrapper>();
        count = 0;

        //grouping.. to aux list
        for (TaskWrapper tw : listTW) {
          //according...
          if (groupBy_searchSortBy == 'By Date' && tw.followUpDate == currentVal) {
            auxlsTW.add(tw);
            count++;
          }
        }

        //add aux list to new group
        if (auxlsTW.size() > 0)
          lsGroup.add(new GroupTasksWrapper(currentVal.format(), auxlsTW, count));
      }

    return lsGroup;
  }

  public static List<TaskWrapper> selectRowsListPagination(List<TaskWrapper> listTW, Integer pageSize) {
    system.debug('## selectRowsListPagination()');

    Integer totalItems = listTW.size();
    pageSize = (pageSize > 0) ? pageSize : 10;
    Integer totalPage = (Integer) Math.ceil((Double) totalItems / (Double) pageSize);
    List<TaskWrapper> auxlsTW = new List<TaskWrapper>();
    Integer i = 0;

    for (TaskWrapper tw : listTW) {
      i++;
      if (i <= pageSize) {
        auxlsTW.add(tw);
        system.debug('## auxlsTW.add(tw)!!!!!');
      } else
        break;
    }

    system.debug('## auxlsTW.size() = ' + auxlsTW.size());
    return auxlsTW;
  }

  //Wrapper for traces
  global class TaskWrapper implements Comparable {
    //Common..
    public String taskId { get; set; }
    public String bidId { get; set; }
    public String serviceId { get; set; }
    public String priority { get; set; }
    public Date followUpDate { get; set; }
    public String city { get; set; }
    public String production { get; set; }
    public String productionId { get; set; }
    public String companies { get; set; }
    public String companiesId { get; set; }
    public String vendor { get; set; }
    public String vendorId { get; set; }
    public String status { get; set; }
    public String coordinator { get; set; }
    public Date deadlineDate { get; set; }

    //Housing
    public Date checkInDate { get; set; }
    public Date checkOutDate { get; set; }

    //GT, Freight
    public Date tripStartDate_gtfr { get; set; }
    public Date tripEndDate_gtfr { get; set; }
    public String tripDescription_gtfr { get; set; }
    public String tripServiceType_gtfr { get; set; }

    //Air
    public Date tripStartDate_air { get; set; }
    public Date tripEndDate_air { get; set; }
    public String tripDescription_air { get; set; }
    public String tripGroupType_air { get; set; }
    public String tripType_air { get; set; }

    public TaskWrapper(
      String taskId,
      String bidId,
      String serviceId,
      String priority,
      Date followUpDate,
      String city,
      String production,
      String productionId,
      String companies,
      String companiesId,
      String vendor,
      String vendorId,
      String status,
      String coordinator,
      Date deadlineDate,
      Date checkInDate,
      Date checkOutDate,
      Date tripStartDate_gtfr,
      Date tripEndDate_gtfr,
      String tripDescription_gtfr,
      String tripServiceType_gtfr,
      Date tripStartDate_air,
      Date tripEndDate_air,
      String tripDescription_air,
      String tripGroupType_air,
      String tripType_air
    ) {
      this.taskId = taskId;
      this.bidId = bidId;
      this.serviceId = serviceId;
      this.priority = priority;
      this.followUpDate = followUpDate;
      this.city = city;
      this.production = production;
      this.productionId = productionId;
      this.companies = companies;
      this.companiesId = companiesId;
      this.vendor = vendor;
      this.vendorId = vendorId;
      this.status = status;
      this.coordinator = coordinator;
      this.deadlineDate = deadlineDate;
      this.checkInDate = checkInDate;
      this.checkOutDate = checkOutDate;
      this.tripStartDate_gtfr = tripStartDate_gtfr;
      this.tripEndDate_gtfr = tripEndDate_gtfr;
      this.tripDescription_gtfr = tripDescription_gtfr;
      this.tripServiceType_gtfr = tripServiceType_gtfr;
      this.tripStartDate_air = tripStartDate_air;
      this.tripEndDate_air = tripEndDate_air;
      this.tripDescription_air = tripDescription_air;
      this.tripGroupType_air = tripGroupType_air;
      this.tripType_air = tripType_air;
    }

    public Integer compareTo(Object compareTo) {
      TaskWrapper compareToGoal = (TaskWrapper) compareTo;
      Integer returnValue = 0;

      //sort
      if (searchSortBy == 'By Status') {
        if (status > compareToGoal.status)
          returnValue = 1;
        else if (status < compareToGoal.status)
          returnValue = -1;
      } else if (searchSortBy == 'By Production') {
        if (production > compareToGoal.production)
          returnValue = 1;
        else if (production < compareToGoal.production)
          returnValue = -1;
      } else if (searchSortBy == 'By Company') {
        if (companies > compareToGoal.companies)
          returnValue = 1;
        else if (companies < compareToGoal.companies)
          returnValue = -1;
      } else if (searchSortBy == 'By City') {
        if (city > compareToGoal.city)
          returnValue = 1;
        else if (city < compareToGoal.city)
          returnValue = -1;
      } else if (searchSortBy == 'By Date') {
        if (followUpDate > compareToGoal.followUpDate)
          returnValue = 1;
        else if (followUpDate < compareToGoal.followUpDate)
          returnValue = -1;
      } else if (searchSortBy == 'By Coordinator') {
        if (coordinator > compareToGoal.coordinator)
          returnValue = 1;
        else if (coordinator < compareToGoal.coordinator)
          returnValue = -1;
      } else if (searchSortBy == 'By Vendor') {
        if (vendor > compareToGoal.vendor)
          returnValue = 1;
        else if (vendor < compareToGoal.vendor)
          returnValue = -1;
      }

      return returnValue;
    }
  }

  global class GroupTasksWrapper {
    public String groupTitle { get; set; }
    public List<TaskWrapper> lsTasks { get; set; }
    public Integer totalTasks { get; set; }

    public GroupTasksWrapper(String groupTitle, List<TaskWrapper> lsTasks, Integer totalTasks) {
      this.groupTitle = groupTitle;
      this.lsTasks = lsTasks;
      this.totalTasks = totalTasks;
    }
  }
}
```


# Last Modified


# Usage

---
layout: default
title: Dashboard_Tab_Contract_Forms
parent: classes
---

```public class Dashboard_Tab_Contract_Forms {
  public User user { get; set; }
  public String bidContractId { get; set; }
  public String bidParentCode { get; set; }
  public String bidParentSObject { get; set; }
  public String dashboard { get; set; }
  public String formLabel { get; set; }
  public String formValue { get; set; }
  public String draftCode { get; set; }
  public Bid__c formBid { get; set; }
  public Account vendor { get; set; }
  public Draft__c draft { get; set; }
  public Date bidStartDate { get; set; }
  public Date GCID_ArrivalDate { get; set; }
  public Date GCID_DepartureDate { get; set; }
  public Date bidEndDate { get; set; }
  public Contact clientContact { get; set; }
  public Contact contractSignerContact { get; set; }
  public Contact contactPrimaryBid { get; set; }
  public String primaryCoordinatorName { get; set; }
  private Air__c firstBidItinerarySegment;
  public List<Dashboard_Tab_Contract_Forms.FormWrapper> formList1 { get; set; }
  public List<Dashboard_Tab_Contract_Forms.FormWrapper> formList2 { get; set; }
  private Map<String, String> symbolsMap;
  private String airSegmentCities;
  ///BidAgreement
  public Boolean isBidAgreementRendered { get; set; }
  public List<SObject> bidAgreementSubTrips { get; set; }
  public List<SObject> bidAgreementVehicles { get; set; }
  public List<Concessions__c> bidAgreementConcessions { get; set; }
  public Revenue__c bidAgreementRevenue { get; set; }
  public String journal_bidjournalRT { get; set; }
  public SObject bidAgreementPrimaryContact { get; set; }
  public Contact bidAgreementAttentionContact { get; set; }
  public String bidAgreement_congaQueriesJson { get; set; }
  public String bidAgreement_congaEmailFromId { get; set; }
  public String bidAgreement_congaEmailTemplateId { get; set; }
  public String bidAgreement_congaTemplateId { get; set; }
  public String bidAgreement_congaSignTemplateId { get; set; }
  public List<SelectOption> dataContactPL { get; set; }
  public Boolean isNew { get; set; }
  public String form_to { get; set; }
  public String form_cc { get; set; }
  public String form_bcc { get; set; }
  public String form_subject { get; set; }
  public String form_body { get; set; }
  public String form_attachs { get; set; }
  public Boolean isCongaSignSent { get; set; }
  public String emailResult { get; set; }
  public List<SelectOption> form_attentionList { get; set; }          //Changes Added as per 175349270
  public String form_attention { get; set; }                          //Changes Added as per 175349270
  public Task form_gcip_new_task { get; set; }                        //Changes Added as per 175349270
  public List<DashboardController.wrapperTask> form_gcip_details_wrapper { get; set; }   
  public String form_date { get; set; }                                                                          //Changes as per 175349270
  public String form_date_gcip_arrival { get; set; }                                                             //Changes as per 175349270
  public String form_date_gcip_departure { get; set; }                                                           //Changes as per 175349270
  public String bidAgreementAttentionContact_Email { get; set; }                                                 //Changes as per 175349270
  public String bidAgreementAttentionContact_Title { get; set; }                                                 //Changes as per 175349270
  public String bidAgreementAttentionContact_Fax { get; set; }                                                   //Changes as per 175349270
  public String bidAgreementAttentionContact_Salutation { get; set; }                                            //Changes as per 175349270
  public String emailAttachs { get; set; }                                                                       //Changes as per 175349270
  public String form_closing { get; set; }                                                                       //Changes as per 175349270
  public string emailMessage  { get; set; }                                                                      //Changes as per 175349270
  //Attach GCQ
  public Boolean isAttachGCQRendered { get; set; }
  public Map<SObject, List<SObject>> gcqSubtripsMap { get; set; }
  public Map<Id, SObject> bidSubtripsMap { get; set; }
  public Boolean isGcqEmpty { get; set; }
  public Boolean isGcqSearched { get; set; }
  public String attachGcq_departureDate { get; set; }
  public String attachGcq_arrivalDate { get; set; }
  public Map<Id, GcqWrapper> searchGcqsMap { get; set; }
  public String selectedGcqId { get; set; }
  //Attachs
  public Boolean isAttachsRendered { get; set; }
  public String filename { get; set; }
  transient public String body { get; set; }
  public List<ContentDocument> attachDocumentList { get; set; }
  public String attachdocument_objectid { get; set; }
  public String newattachment_id { get; set; }
  public String newattachment_name { get; set; }
  public List<ContentDocument> documentBidList { get; set; }
  public Integer documentListFirst { get; set; }
  public Integer documentListPage { get; set; }
  public Integer documentListLastPage { get; set; }
  public List<Integer> documentListPages { get; set; }
  public String documentRelationId { get; set; }
  public List<Task> form_gcip_details { get; set; }                                       //Changes Added as per 175349270
  public Dashboard_Tab_Contract_Forms() {
    isBidAgreementRendered = isAttachsRendered = isAttachGCQRendered = isCongaSignSent = false;
    bidAgreementPrimaryContact = bidAgreementAttentionContact = new Contact();
    dataContactPL = new List<SelectOption>();
  }
  public void loadForms() {
    //Changes as per 175349270
    bidAgreementAttentionContact_Fax = '';
    bidAgreementAttentionContact_Email = '';
    bidAgreementAttentionContact_Title = '';
    bidAgreementAttentionContact_Salutation = '';
    form_attentionList = new List<SelectOption>();
    form_gcip_details_wrapper = new List<DashboardController.wrapperTask>();
    form_gcip_details = new List<Task>();
    formList1 = new List<Dashboard_Tab_Contract_Forms.FormWrapper>();
    formList2 = new List<Dashboard_Tab_Contract_Forms.FormWrapper>();
    List<Bid__c> searchBid = new List<Bid__c>();
    dashboard = bidParentSObject == 'Ground' ? 'GT' : bidParentSObject;
    if (bidParentSObject == 'Ground')
      searchBid = [
        SELECT
          Id,
          Name,
          RecordTypeId,
          Form_Cancellation_Letter__c,
          Form_Create_GCIP__c,              //Changes Added as per 175349270
          Form_Contract_Date_Change__c,
          Form_Contract_to_Client__c,
          Form_Counter_Needed__c,
          Form_Credit_Card_Change__c,
          Form_Email_Confirmation__c,
          Form_Final_Contract__c,
          Form_GCIP__c,
          //Fix By Clay 28 Dec, 2020
          Form_GT_GCIP__c,
          Form_Housing_Contract__c,
          Form_No_Pick_Up__c,
          Form_Pick_Up_Report__c,
          Form_Rate_Agreement__c,
          Form_Room_Changes__c,
          Form_Rooming_List_Reminder__c,
          Form_Transportation_Contract__c,
          Form_Trip_Details_Update__c,
          GT__c,
          GT__r.Name,
          GT__r.Start_Date__c,
          GT__r.End_Date__c,
          GT__r.Description__c,
          Vendor_Contact__c,
          Vendor__c,
          Vendor__r.Vendor_ID__c,
          Vendor__r.ParentId,
          Vendor__r.Name,
          Vendor_Address__c,
          Production__c,
          Production__r.Name,
          Production__r.Production_ID__c,
          Production__r.Account.Name,
          Production__r.Account.Physical_Address__c,
          Production__r.Office_Location__c,
          Contracting_Back_End_Coordinator__c,
          Contracting_Back_End_Coordinator__r.Name,
          Contracting_Back_End_Coordinator__r.Email,
          Contracting_Back_End_Coordinator__r.Phone,
          CreatedBy.Name,                                       //Changes Added as per 175349270
          CreatedDate,                                          //Changes Added as per 175349270
          LastModifiedDate,                                     //Changes Added as per 175349270
          LastModifiedBy.Name,                                  //Changes Added as per 175349270
          Housing__r.Date_In__c,                                //Changes Added as per 175349270
          Housing__r.Date_Out__c,                               //Changes Added as per 175349270
          Form_Create_GCIP_Last_Send_Date__c,                   //Changes Added as per 175349270
          Housing__c                                            //Changes Added as per 175349270
        FROM Bid__c
        WHERE Id = :bidContractId
      ];
    else if (bidParentSObject == 'Freight')
      searchBid = [
        SELECT
          Id,
          Name,
          RecordTypeId,
          Form_Cancellation_Letter__c,
          Form_Contract_Date_Change__c,
          Form_Contract_to_Client__c,
          Form_Counter_Needed__c,
          Form_Credit_Card_Change__c,
          Form_Email_Confirmation__c,
          Form_Final_Contract__c,
          Form_GCIP__c,
          Form_Housing_Contract__c,
          Form_No_Pick_Up__c,
          Form_Pick_Up_Report__c,
          Form_Rate_Agreement__c,
          Form_Room_Changes__c,
          Form_Rooming_List_Reminder__c,
          Form_Transportation_Contract__c,
          Form_Trip_Details_Update__c,
          Freight__c,
          Freight__r.Name,
          Freight__r.Start_Date__c,
          Freight__r.End_Date__c,
          Freight__r.Description__c,
          Vendor_Contact__c,
          Vendor__c,
          Vendor__r.Vendor_ID__c,
          Vendor__r.ParentId,
          Vendor__r.Name,
          Vendor_Address__c,
          Production__c,
          Production__r.Name,
          Production__r.Production_ID__c,
          Production__r.Account.Name,
          Production__r.Account.Physical_Address__c,
          Production__r.Office_Location__c,
          Contracting_Back_End_Coordinator__c,
          Contracting_Back_End_Coordinator__r.Name,
          Contracting_Back_End_Coordinator__r.Email,
          Contracting_Back_End_Coordinator__r.Phone
        FROM Bid__c
        WHERE Id = :bidContractId
      ];
    else if (bidParentSObject == 'Air')
      searchBid = [
        SELECT
          Id,
          Name,
          RecordTypeId,
          Client_Deposit_Due_Date__c,
          Client_Utilization_Date__c,
          Client_Names_Final_Payment__c,
          Deposit_Amount_per_seat__c,
          Deposit_Amount_Currency__c,
          Utilization_Percentage__c,
          Utilization_Penalty_per_seat__c,
          Utilization_Penalty_Currency__c,
          Air__c,
          Freight__c,
          Air__r.Name,
          Air__r.Departure_Date__c,
          Air__r.Arrival_Date__c,
          Air__r.Return_Date__c,
          Air__r.Description__c,
          Air__r.Group_Type__c,
          Form_Deposit_Due__c,
          Form_Utilization__c,
          Form_Names_Final_Payment__c,
          Form_Final_Choice__c,
          Form_Ticketed_Confirmation__c,     
          Form_Final_Air_Confirmation__c,
          Vendor_Contact__c,
          Vendor__c,
          Vendor__r.Vendor_ID__c,
          Vendor__r.ParentId,
          Vendor__r.Name,
          Vendor_Address__c,
          Production__c,
          Production__r.Name,
          Production__r.Production_ID__c,
          Production__r.Account.Name,
          Production__r.Account.Physical_Address__c,
          Contracting_Back_End_Coordinator__c,
          Contracting_Back_End_Coordinator__r.Name,
          Contracting_Back_End_Coordinator__r.Email,
          Contracting_Back_End_Coordinator__r.Phone
        FROM Bid__c
        WHERE Id = :bidContractId
      ];
    formBid = !searchBid.isEmpty() ? searchBid.get(0) : new Bid__c();
    Map<String, Production_Associations__c> productionContactsMap = new Map<String, Production_Associations__c>();
    for (Production_Associations__c productionContact : [
      SELECT Id, Contact__c, Contact__r.Name,Contact__r.Fax,Contact__r.Email,Contact__r.Title, Role__c, Contact__r.FirstName
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :formBid.Production__c
        AND RecordType.DeveloperName = 'Production_Contacts'
        AND Contact__c != NULL
        AND Role__c INCLUDES (:('Primary ' + dashboard), 'Contract Signer')
    ]) {
      form_attentionList.add(new SelectOption(productionContact.Contact__c, productionContact.Contact__r.Name));          //Changes Added as per 175349270
      bidAgreementAttentionContact_Email = productionContact.Contact__r.Email;
      bidAgreementAttentionContact_Title = productionContact.Contact__r.Title;
      bidAgreementAttentionContact_Fax = productionContact.Contact__r.Fax;
      bidAgreementAttentionContact_Salutation = productionContact.Contact__r.FirstName;
      form_attention = productionContact.Contact__c;
      if (productionContact.Role__c.contains('Primary ' + dashboard))
        productionContactsMap.put('Primary ' + dashboard, productionContact);
      if (productionContact.Role__c.contains('Contract Signer'))
        productionContactsMap.put('Contract Signer', productionContact);
    }
    clientContact = productionContactsMap.containsKey('Primary ' + dashboard)
      ? productionContactsMap.get('Primary ' + dashboard).Contact__r
      : new Contact();
    contractSignerContact = productionContactsMap.containsKey('Contract Signer')
      ? productionContactsMap.get('Contract Signer').Contact__r
      : new Contact();
    contactPrimaryBid = formBid.Vendor_Contact__c != null
      ? [
          SELECT Id, FirstName, Name, Phone, Email
          FROM Contact
          WHERE Id = :formBid.Vendor_Contact__c
          LIMIT 1
        ]
      : new Contact();
    vendor = formBid.Vendor__c != null
      ? [
          SELECT Id, Name, Email__c, City__c, City__r.Name
          FROM Account
          WHERE Id = :formBid.Vendor__c
          LIMIT 1
        ]
      : new Account();
    primaryCoordinatorName = '';
    switch on bidParentSObject {
      when 'Ground' {
        formList1.add(
          new FormWrapper(
            'Rate Agreement',
            'Form_Rate_Agreement__c',
            formBid.Form_Rate_Agreement__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Contract To Client',
            'Form_Contract_to_Client__c',
            formBid.Form_Contract_to_Client__c
          )
        );
        formList1.add(                            //Changes Added as per 175349270
          new FormWrapper(
            'Ground Transportation Procedures',
            'Form_Create_GCIP__c',
            //Fix By Clay 29 Dec, 2020
            //formBid.Form_Create_GCIP__c
            formBid.Form_GT_GCIP__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Counter Needed',
            'Form_Counter_Needed__c',
            formBid.Form_Counter_Needed__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Final Contract',
            'Form_Final_Contract__c',
            formBid.Form_Final_Contract__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Send Signer',
            'Send Signer',
            formBid.Form_Final_Contract__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Transportation Contract',
            'Form_Transportation_Contract__c',
            formBid.Form_Transportation_Contract__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Trip Details Update',
            'Form_Trip_Details_Update__c',
            formBid.Form_Trip_Details_Update__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Credit Card Change',
            'Form_Credit_Card_Change__c',
            formBid.Form_Credit_Card_Change__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Email Confirmation',
            'Form_Email_Confirmation__c',
            formBid.Form_Email_Confirmation__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Cancellation',
            'Form_Cancellation_Letter__c',
            formBid.Form_Cancellation_Letter__c
          )
        );

        bidParentCode = formBid.GT__r.Name;
        bidStartDate = formBid.GT__r.Start_Date__c != null
          ? formBid.GT__r.Start_Date__c
          : null;
        bidEndDate = formBid.GT__r.End_Date__c != null
          ? formBid.GT__r.End_Date__c
          : null;
        User emailFromUser = verifyEmailUser(UserInfo.getUserId());
        primaryCoordinatorName = emailFromUser.Name;
        bidAgreement_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
      }
      when 'Freight' {
        formList1.add(
          new FormWrapper(
            'Rate Agreement',
            'Form_Rate_Agreement__c',
            formBid.Form_Rate_Agreement__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Contract To Client',
            'Form_Contract_to_Client__c',
            formBid.Form_Contract_to_Client__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Counter Needed',
            'Form_Counter_Needed__c',
            formBid.Form_Counter_Needed__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Final Contract',
            'Form_Final_Contract__c',
            formBid.Form_Final_Contract__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Send Signer',
            'Send Signer',
            formBid.Form_Final_Contract__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Transportation Contract',
            'Form_Transportation_Contract__c',
            formBid.Form_Transportation_Contract__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Trip Details Update',
            'Form_Trip_Details_Update__c',
            formBid.Form_Trip_Details_Update__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Credit Card Change',
            'Form_Credit_Card_Change__c',
            formBid.Form_Credit_Card_Change__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Email Confirmation',
            'Form_Email_Confirmation__c',
            formBid.Form_Email_Confirmation__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Cancellation',
            'Form_Cancellation_Letter__c',
            formBid.Form_Cancellation_Letter__c
          )
        );
        bidParentCode = formBid.Freight__r.Name;
        bidStartDate = formBid.Freight__r.Start_Date__c != null
          ? formBid.Freight__r.Start_Date__c
          : null;
        bidEndDate = formBid.Freight__r.End_Date__c != null
          ? formBid.Freight__r.End_Date__c
          : null;
        User emailFromUser = verifyEmailUser(UserInfo.getUserId());
        primaryCoordinatorName = emailFromUser.Name;
        bidAgreement_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
      }
      when 'Air' {
        formList1.add(
          new FormWrapper(
            'Deposit Due',
            'Form_Deposit_Due__c',
            formBid.Form_Deposit_Due__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Utilization',
            'Form_Utilization__c',
            formBid.Form_Utilization__c
          )
        );
        formList1.add(
          new FormWrapper(
            'Names & Final Payment',
            'Form_Names_Final_Payment__c',
            formBid.Form_Names_Final_Payment__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Final Choice',
            'Form_Final_Choice__c',
            formBid.Form_Final_Choice__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Ticketed Confirmation',
            'Form_Ticketed_Confirmation__c',
            formBid.Form_Ticketed_Confirmation__c
          )
        );
        formList2.add(
          new FormWrapper(
            'Final Air Confirmation',
            'Form_Final_Air_Confirmation__c',
            formBid.Form_Final_Air_Confirmation__c
          )
        );
        
        bidParentCode = formBid.Air__r.Name;
        bidStartDate = formBid.Air__r.Departure_Date__c != null
          ? formBid.Air__r.Departure_Date__c
          : null;
        bidEndDate = formBid.Air__r.Return_Date__c != null
          ? formBid.Air__r.Return_Date__c
          : null;
        User emailFromUser = verifyEmailUser(UserInfo.getUserId());
        primaryCoordinatorName = emailFromUser.Name;
        bidAgreement_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
        List<Air__c> bidItinerarySegments = new List<Air__c>();
        for (Air__c segment : [
          SELECT id, Equip_Type__c
          FROM Air__c
          WHERE
            Air_Itinerary_Details__r.Bid_Itinerary__c = :formBid.id
            AND RecordType.DeveloperName = 'Air_Segments'
          ORDER BY Order__c
          LIMIT 1
        ])
          bidItinerarySegments.add(segment);
        firstBidItinerarySegment = !bidItinerarySegments.isEmpty()
          ? bidItinerarySegments[0]
          : new Air__c();
        symbolsMap = new Map<String, String>{
          'AED' => 'د.إ',
          'AFN' => 'Af',
          'ALL' => 'L',
          'AMD' => 'Դ',
          'AOA' => 'Kz',
          'ARS' => '$',
          'AUD' => '$',
          'AWG' => 'ƒ',
          'AZN' => 'ман',
          'BAM' => 'КМ',
          'BBD' => '$',
          'BDT' => '৳',
          'BGN' => 'лв',
          'BHD' => 'ب.د',
          'BIF' => '₣',
          'BMD' => '$',
          'BND' => '$',
          'BOB' => 'Bs.',
          'BRL' => 'R$',
          'BSD' => '$',
          'BTN' => '',
          'BWP' => 'P',
          'BYN' => 'Br',
          'BZD' => '$',
          'CAD' => '$',
          'CDF' => '₣',
          'CHF' => '₣',
          'CLP' => '$',
          'CNY' => '¥',
          'COP' => '$',
          'CRC' => '₡',
          'CUP' => '$',
          'CVE' => '$',
          'CZK' => 'Kč',
          'DJF' => '₣',
          'DKK' => 'kr',
          'DOP' => '$',
          'DZD' => 'د.ج',
          'EGP' => '£',
          'ERN' => 'Nfk',
          'ETB' => '',
          'EUR' => '€',
          'FJD' => '$',
          'FKP' => '£',
          'GBP' => '£',
          'GEL' => 'ლ',
          'GHS' => '₵',
          'GIP' => '£',
          'GMD' => 'D',
          'GNF' => '₣',
          'GTQ' => 'Q',
          'GYD' => '$',
          'HKD' => '$',
          'HNL' => 'L',
          'HRK' => 'Kn',
          'HTG' => 'G',
          'HUF' => 'Ft',
          'IDR' => 'Rp',
          'ILS' => '₪',
          'INR' => '₹',
          'IQD' => 'ع.د',
          'IRR' => '﷼',
          'ISK' => 'Kr',
          'JMD' => '$',
          'JOD' => 'د.ا',
          'JPY' => '¥',
          'KES' => 'Sh',
          'KGS' => '',
          'KHR' => '៛',
          'KPW' => '₩',
          'KRW' => '₩',
          'KWD' => 'د.ك',
          'KYD' => '$',
          'KZT' => '〒',
          'LAK' => '₭',
          'LBP' => 'ل.ل',
          'LKR' => 'Rs',
          'LRD' => '$',
          'LSL' => 'L',
          'LYD' => 'ل.د',
          'MAD' => 'د.م.',
          'MDL' => 'L',
          'MGA' => '',
          'MKD' => 'ден',
          'MMK' => 'K',
          'MNT' => '₮',
          'MOP' => 'P',
          'MRU' => 'UM',
          'MUR' => '₨',
          'MVR' => 'ރ.',
          'MWK' => 'MK',
          'MXN' => '$',
          'MYR' => 'RM',
          'MZN' => 'MTn',
          'NAD' => '$',
          'NGN' => '₦',
          'NIO' => 'C$',
          'NOK' => 'kr',
          'NPR' => '₨',
          'NZD' => '$',
          'OMR' => 'ر.ع.',
          'PAB' => 'B/.',
          'PEN' => 'S/.',
          'PGK' => 'K',
          'PHP' => '₱',
          'PKR' => '₨',
          'PLN' => 'zł',
          'PYG' => '₲',
          'QAR' => 'ر.ق',
          'RON' => 'L',
          'RSD' => 'din',
          'RUB' => 'р.',
          'RWF' => '₣',
          'SAR' => 'ر.س',
          'SBD' => '$',
          'SCR' => '₨',
          'SDG' => '£',
          'SEK' => 'kr',
          'SGD' => '$',
          'SHP' => '£',
          'SLL' => 'Le',
          'SOS' => 'Sh',
          'SRD' => '$',
          'STN' => 'Db',
          'SYP' => 'ل.س',
          'SZL' => 'L',
          'THB' => '฿',
          'TJS' => 'ЅМ',
          'TMT' => 'm',
          'TND' => 'د.ت',
          'TOP' => 'T$',
          'TRY' => '₤',
          'TTD' => '$',
          'TWD' => '$',
          'TZS' => 'Sh',
          'UAH' => '₴',
          'UGX' => 'Sh',
          'USD' => '$',
          'UYU' => '$',
          'UZS' => '',
          'VEF' => 'Bs F',
          'VND' => '₫',
          'VUV' => 'Vt',
          'WST' => 'T',
          'XAF' => '₣',
          'XCD' => '$',
          'XPF' => '₣',
          'YER' => '﷼',
          'ZAR' => 'R',
          'ZMW' => 'ZK',
          'ZWL' => '$'
        };
      }
    }
    isBidAgreementRendered = isAttachsRendered = isAttachGCQRendered = false;
  }
  public void bindAttentionDetails(){                                                                           //Changes Added as per 175349270
    System.debug('Selected Contact: '+ form_attention);
    List<Contact> Contact = [Select FirstName, Email, fax, Title from Contact where Id=:form_attention];
    bidAgreementAttentionContact_Fax = Contact[0].Fax;
    bidAgreementAttentionContact_Email = Contact[0].Email;
    bidAgreementAttentionContact_Title = Contact[0].Title;
    bidAgreementAttentionContact_Salutation = 'Hello '+Contact[0].FirstName+',';
  }
  public void newFormGCIPTask() {                                                                             //Changes Added as per 175349270
    Id taskRecordTypeGCIPId = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName()
      .get('GCIP')
      .getRecordTypeId();
     form_gcip_new_task = new Task(
      OwnerId = UserInfo.getUserId(),
      RecordTypeId = taskRecordTypeGCIPId,
      WhatId = bidContractId
    );
  }
  ///BidAgreement Methods
  public void openForm() {
    Bid__c bid = String.isNotEmpty(formBid.Id)
      ? [
          SELECT
            id,
            Vendor__c,
            Vendor__r.Payment_policy__c,
            Vendor__r.Cancellation_Policy__c,
            Rate_Agreement_Last_Send_Date__c,
            Form_Create_GCIP_Last_Send_Date__c,         //Changes Added as per 175349270
            Rate_Agreement_Last_Send_By__c,
            Trip_Details_Update_Last_Send_Date__c,
            Trip_Details_Update_Last_Send_By__c,
            Transportation_Contract_Last_Send_Date__c,
            Transportation_Contract_Last_Send_By__c,
            Contract_to_Client_Last_Send_Date__c,
            Contract_to_Client_Last_Send_By__c,
            Counter_Needed_Last_Send_Date__c,
            Counter_Needed_Last_Send_By__c,
            Final_Contract_Last_Send_Date__c,
            Final_Contract_Last_Send_By__c,
            Email_Confirmation_Last_Send_By__c,
            Email_Confirmation_Last_Send_Date__c,
            Credit_Card_Last_Send_Date__c,
            Credit_Card_Last_Send_By__c,
            Cancellation_Last_Send_Date__c,
            Cancellation_Last_Send_By__c,
            Deposit_Due_Last_Send_Date__c,
            Deposit_Due_Last_Send_By__c,
            Utilization_Last_Send_Date__c,
            Utilization_Last_Send_By__c,
            Names_Final_Payment_Last_Send_Date__c,
            Names_Final_Payment_Last_Send_By__c,
            Final_Choice_Last_Send_Date__c,
            Final_Choice_Last_Send_By__c,
            Ticketed_Confirmation_Last_Send_Date__c,
            Ticketed_Confirmation_Last_Send_By__c,
            Final_Air_Confirmation_Last_Send_Date__c,
            Final_Air_Confirmation_Last_Send_By__c
          FROM Bid__c
          WHERE id = :formBid.Id
        ]
      : new Bid__c();
    user = [
      SELECT id, Housing_Preference__c
      FROM User
      WHERE id = :UserInfo.getUserId()
    ];
    List<Revenue__c> bidRevenues = [
      SELECT id, Gratuity__c, Total_Price__c
      FROM Revenue__c
      WHERE
        Bid__c = :formBid.id
        AND RecordType.DeveloperName = :(bidParentSObject == 'Ground'
          ? 'Ground_Rate_Travel_Commission'
          : bidParentSObject == 'Freight'
              ? 'Freight_Rate_Commission'
              : bidParentSObject == 'Air' ? 'Air_Rate_Commission' : '')
      ORDER BY createdDate DESC
      LIMIT 1
    ];
    bidAgreementRevenue = !bidRevenues.isEmpty()
      ? bidRevenues[0]
      : new Revenue__c();
    formBid.put(
      formValue == 'Form_Rate_Agreement__c'
        ? 'Rate_Agreement_Last_Send_Date__c'
        : formValue == 'Form_Trip_Details_Update__c'
            ? 'Trip_Details_Update_Last_Send_Date__c'
            : formValue == 'Form_Transportation_Contract__c'
                ? 'Transportation_Contract_Last_Send_Date__c'
                : formValue == 'Form_Contract_to_Client__c'
                    ? 'Contract_to_Client_Last_Send_Date__c'
                    : formValue == 'Form_Counter_Needed__c'
                        ? 'Counter_Needed_Last_Send_Date__c'
                        : formValue == 'Form_Final_Contract__c'
                            ? 'Final_Contract_Last_Send_Date__c'
                            : formValue == 'Form_Email_Confirmation__c'
                                ? 'Email_Confirmation_Last_Send_Date__c'
                                : formValue == 'Form_Credit_Card_Change__c'
                                    ? 'Credit_Card_Last_Send_Date__c'
                                    : formValue == 'Form_Cancellation_Letter__c'
                                        ? 'Cancellation_Last_Send_Date__c'
                                        : formValue == 'Form_Deposit_Due__c'
                                            ? 'Deposit_Due_Last_Send_Date__c'
                                            : formValue == 'Form_Utilization__c'
                                                ? 'Utilization_Last_Send_Date__c'
                                                : formValue ==
                                                    'Form_Names_Final_Payment__c'
                                                    ? 'Names_Final_Payment_Last_Send_Date__c'
                                                    : formValue ==
                                                        'Form_Final_Choice__c'
                                                        ? 'Final_Choice_Last_Send_Date__c'
                                                        : formValue ==
                                                            'Form_Ticketed_Confirmation__c'
                                                            ? 'Ticketed_Confirmation_Last_Send_Date__c'
                                                            : formValue ==                                  //Changes Added as per 175349270
                                                            'Form_Create_GCIP__c'
                                                            ? 'Form_Create_GCIP_Last_Send_Date__c'
                                                            : formValue ==
                                                                'Form_Final_Air_Confirmation__c'
                                                                ? 'Final_Air_Confirmation_Last_Send_Date__c'
                                                                : '',
      formValue == 'Form_Rate_Agreement__c'
        ? bid.Rate_Agreement_Last_Send_Date__c
        : formValue == 'Form_Trip_Details_Update__c'
            ? bid.Trip_Details_Update_Last_Send_Date__c
            : formValue == 'Form_Transportation_Contract__c'
                ? bid.Transportation_Contract_Last_Send_Date__c
                : formValue == 'Form_Contract_to_Client__c'
                    ? bid.Contract_to_Client_Last_Send_Date__c
                    : formValue == 'Form_Counter_Needed__c'
                        ? bid.Counter_Needed_Last_Send_Date__c
                        : formValue == 'Form_Final_Contract__c'
                            ? bid.Final_Contract_Last_Send_Date__c
                            : formValue == 'Form_Email_Confirmation__c'
                                ? bid.Email_Confirmation_Last_Send_Date__c
                                : formValue == 'Form_Credit_Card_Change__c'
                                    ? bid.Credit_Card_Last_Send_Date__c
                                    : formValue == 'Form_Cancellation_Letter__c'
                                        ? bid.Cancellation_Last_Send_Date__c
                                        : formValue == 'Form_Deposit_Due__c'
                                            ? bid.Deposit_Due_Last_Send_Date__c
                                            : formValue == 'Form_Utilization__c'
                                                ? bid.Utilization_Last_Send_Date__c
                                                : formValue ==
                                                    'Form_Names_Final_Payment__c'
                                                    ? bid.Names_Final_Payment_Last_Send_Date__c
                                                    : formValue ==
                                                        'Form_Final_Choice__c'
                                                        ? bid.Final_Choice_Last_Send_Date__c
                                                        : formValue ==
                                                            'Form_Ticketed_Confirmation__c'
                                                            ? bid.Ticketed_Confirmation_Last_Send_Date__c
                                                            /*: formValue ==
                                                            'Form_Create_GCIP__c '                                        //Changes Added as per 175349270
                                                            ? bid.Form_Create_GCIP_Last_Send_Date__c 
                                                            */
                                                            : formValue ==
                                                                'Form_Final_Air_Confirmation__c'
                                                                ? bid.Final_Air_Confirmation_Last_Send_Date__c
                                                                : null
    );
    formBid.put(
      formValue == 'Form_Rate_Agreement__c'
        ? 'Rate_Agreement_Last_Send_By__c'
        : formValue == 'Form_Trip_Details_Update__c'
            ? 'Trip_Details_Update_Last_Send_By__c'
            : formValue == 'Form_Transportation_Contract__c'
                ? 'Transportation_Contract_Last_Send_By__c'
                : formValue == 'Form_Contract_to_Client__c'
                    ? 'Contract_to_Client_Last_Send_By__c'
                    : formValue == 'Form_Counter_Needed__c'
                        ? 'Counter_Needed_Last_Send_By__c'
                        : formValue == 'Form_Final_Contract__c'
                            ? 'Final_Contract_Last_Send_By__c'
                            : formValue == 'Form_Email_Confirmation__c'
                                ? 'Email_Confirmation_Last_Send_By__c'
                                : formValue == 'Form_Credit_Card_Change__c'
                                    ? 'Credit_Card_Last_Send_By__c'
                                    : formValue == 'Form_Cancellation_Letter__c'
                                        ? 'Cancellation_Last_Send_By__c'
                                        : formValue == 'Form_Deposit_Due__c'
                                            ? 'Deposit_Due_Last_Send_By__c'
                                            : formValue == 'Form_Utilization__c'
                                                ? 'Utilization_Last_Send_By__c'
                                                : formValue ==
                                                    'Form_Names_Final_Payment__c'
                                                    ? 'Names_Final_Payment_Last_Send_By__c'
                                                    : formValue ==
                                                        'Form_Final_Choice__c'
                                                        ? 'Final_Choice_Last_Send_By__c'
                                                        : formValue ==
                                                            'Form_Ticketed_Confirmation__c'
                                                            ? 'Ticketed_Confirmation_Last_Send_By__c'
                                                            : formValue ==                                              //Changes Added as per 175349270
                                                            'Form_Create_GCIP__c'
                                                            ? 'Form_Create_GCIP_Last_Send_Date__c'
                                                            : formValue ==
                                                                'Form_Final_Air_Confirmation__c'
                                                                ? 'Final_Air_Confirmation_Last_Send_By__c'
                                                                : '',
      formValue == 'Form_Rate_Agreement__c'
        ? bid.Rate_Agreement_Last_Send_By__c
        : formValue == 'Form_Trip_Details_Update__c'
            ? bid.Trip_Details_Update_Last_Send_By__c
            : formValue == 'Form_Transportation_Contract__c'
                ? bid.Transportation_Contract_Last_Send_By__c
                : formValue == 'Form_Contract_to_Client__c'
                    ? bid.Contract_to_Client_Last_Send_By__c
                    : formValue == 'Form_Counter_Needed__c'
                        ? bid.Counter_Needed_Last_Send_By__c
                        : formValue == 'Form_Final_Contract__c'
                            ? bid.Final_Contract_Last_Send_By__c
                            : formValue == 'Form_Email_Confirmation__c'
                                ? bid.Email_Confirmation_Last_Send_By__c
                                : formValue == 'Form_Credit_Card_Change__c'
                                    ? bid.Credit_Card_Last_Send_By__c
                                    : formValue == 'Form_Cancellation_Letter__c'
                                        ? bid.Cancellation_Last_Send_By__c
                                        : formValue == 'Form_Deposit_Due__c'
                                            ? bid.Deposit_Due_Last_Send_By__c
                                            : formValue == 'Form_Utilization__c'
                                                ? bid.Utilization_Last_Send_By__c
                                                : formValue ==
                                                    'Form_Names_Final_Payment__c'
                                                    ? bid.Names_Final_Payment_Last_Send_By__c
                                                    : formValue ==
                                                        'Form_Final_Choice__c'
                                                        ? bid.Final_Choice_Last_Send_By__c
                                                        : formValue ==
                                                            'Form_Ticketed_Confirmation__c'
                                                            ? bid.Ticketed_Confirmation_Last_Send_By__c
                                                            : formValue == 'Form_Create_GCIP__c'
                                                            ? bid.Form_Create_GCIP_Last_Send_Date__c
                                                            : formValue ==
                                                                'Form_Final_Air_Confirmation__c'
                                                                ? bid.Final_Air_Confirmation_Last_Send_By__c
                                                                : null
    );        //Changes Added as per 175349270
    journal_bidjournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByName()
        .get('Bid Journal') != null
      ? Schema.SObjectType.Journal__c.getRecordTypeInfosByName()
          .get('Bid Journal')
          .getRecordTypeId()
      : null;
    bidAgreementPrimaryContact.clear();
    bidAgreementAttentionContact.clear();
    bidAgreement_congaEmailTemplateId = bidAgreement_congaTemplateId = bidAgreement_congaSignTemplateId = null;
    isNew = false;
    //Fix By Clay 28 Dec, 2020
    Id taskRecordTypeGCIPId = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('GCIP').getRecordTypeId();
    if(bidParentSObject == 'Ground' && formBid.GT__c != NULL) {
        form_date_gcip_arrival = Datetime.newInstance(
        formBid.GT__r.Start_Date__c,
        Time.newInstance(0, 0, 0, 0)
        )
        .format('EEEE, MMMM d, yyyy');
        form_date_gcip_departure = Datetime.newInstance(
        formBid.GT__r.End_Date__c,
        Time.newInstance(0, 0, 0, 0)
        )
        .format('EEEE, MMMM d, yyyy');
    }  
    if (String.isNotBlank(draftCode)) {
      draft = [
        SELECT
          Id,
          Name,
          Salutation__c,
          Attention__c,
          Primary_Contact_Id__c,
          Production_Assoc_Contact_Id__c,
          CC__c,
          Subject__C,
          Date__c,
          BCC__c,
          Body__c,
          Terms__c,
          CreatedBy.Name,
          CreatedDate,
          LastModifiedBy.Name,
          LastModifiedDate,
          Payment_Policy__c,
          Cancellation_Policy__c,
          Production_Assoc_Type__c,
          Credit_Card_Id__c
        FROM Draft__c
        WHERE Name = :draftCode
      ];
    
    //Fix By Clay 29 Dec, 2020
    if(bidParentSObject == 'Ground') {
      if(String.isBlank(formBid.Form_GT_GCIP__c)) {
        Bid__c b = new Bid__c(id=formBid.Id);
        b.Form_GT_GCIP__c = draft.Name;
        update b;
        formBid.Form_GT_GCIP__c = draft.Name;
      }
      if(draft.Date__c != NULL) {
          form_date = Datetime.newInstance(
          draft.Date__c,
          Time.newInstance(0, 0, 0, 0)
          )
          .format('EEEE, MMMM d, yyyy');
      }
      if(form_gcip_details_wrapper.size() == 0) {
          form_gcip_details = [
              SELECT Id, Priority__c, Subject, Description
              FROM Task
              WHERE
              WhatId = :bidContractId
              AND RecordTypeId = :taskRecordTypeGCIPId
              ORDER BY Priority__c ASC
          ];
          if(form_gcip_details.size() >0){
              for(Task t : form_gcip_details){
                  DashboardController.wrapperTask obj = new DashboardController.wrapperTask();
                  obj.Id = t.Id;
                  obj.Priority = String.valueOf(t.Priority__c);
                  obj.Subject = t.Subject;
                  obj.Description = t.Description;
                  String str = t.Description.replace('<ul><li>','
 o  ');
                  str = str.replace('</li></ul>','');
                  str = str.replace('<li>','
 o');
                  str = str.replace('</li>','');
                  obj.DescriptionOutput = str;
                  form_gcip_details_wrapper.add(obj);
              }
          }
      }
    }
  } else {
      isNew = true;
      draft = new Draft__c();
      draft.Salutation__c = 'Hi ,';
      draft.Date__c = Date.today();
       //For GCIP Task Binding                                                        
        if (bidParentSObject == 'Ground'){                                                  //Changes Added as per 175349270  
          /**Fix By Clay 29 Dec, 2020
          DateTime dT = formBid.CreatedDate;
          form_date = String.valueOf(date.newinstance(dT.year(), dT.month(), dT.day()));    
          if(formBid.Housing__c!=NULL){
            form_date_gcip_arrival = Datetime.newInstance(
              formBid.Housing__r.Date_In__c,
              Time.newInstance(0, 0, 0, 0)
            )
            .format('EEEE, MMMM d, yyyy');
            form_date_gcip_departure = Datetime.newInstance(
              formBid.Housing__r.Date_Out__c,
              Time.newInstance(0, 0, 0, 0)
            )
            .format('EEEE, MMMM d, yyyy');
          }    
          //Task Creation + Binding
          Id taskRecordTypeGCIPId = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('GCIP').getRecordTypeId();
          if(formBid.Form_GT_GCIP__c==''){**/
           if(draft.Date__c != NULL) {
                form_date = Datetime.newInstance(
                draft.Date__c,
                Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE, MMMM d, yyyy');
            }
            if(String.isBlank(formBid.Form_GT_GCIP__c)) {
            form_gcip_details = new List<Task>();
                  form_gcip_details.add(
                    new Task(
                      OwnerId = UserInfo.getUserId(),
                      RecordTypeId = taskRecordTypeGCIPId,
                      WhatId = formBid.Id,
                      Priority__c = 10,
                      Subject = 'Bus Company/ Driver Responsibilities',
                      /**Fix By Clay 29 Dec, 2020
                      Description = 
                      '<ul><li>Thorough 32-point invasive deep cleaning including HVAC and ventilation. Buses are to be cleaned according to CDC regulations. Extra attention to be paid to frequently touched areas such as handrails, armrests, interior and exterior door handles, seat belts/buckles, and seats.</li>'+
                      '<li>Drivers are not permitted to work if they are showing any symptom of flu or coronavirus- must notify dispatch immediately if already on tour.</li>'+
                      '<li>Upon boarding the coach, the driver must explain to Group Leader the protocols should anyone become ill during the trip.</li>'+
                      '<li>Always wear gloves when handling luggage.</li>'+
                      '<li>Maintain space from passengers when off and on the bus </li>'+
                      '<li>Always wear a mask while driving, when requested by Group Leader </li>'+
                      '<li>Clean high touch areas with higher-grade disinfectant any time passengers are off the bus.</li>'+
                      '<li>Hand sanitizer stations must be located on board and made readily available to group members.</li>'+
                      '<li>No printed material on board (books, magazines, etc.). </li>'+
                      '<li>Bus company will not supply in-vehicle water or beverages.</li>'+
                      '<li>The row of seats directly behind the driver and across from the driver will be unavailable for seating to ensure social distancing.</li>'+
                      '<li>For overnight/ multi-day travel, clean the bus and lock bus doors with no access allowed until agreed upon time.</li></ul>'
                    	)**/
                      Description = 
                      '<ul><li> Thorough 32-point invasive deep cleaning including HVAC and ventilation. Buses are to be cleaned according to CDC regulations. Extra attention to be paid to frequently touched areas such as handrails, armrests, interior and exterior door handles, seat belts/buckles, and seats.</li>'+
                      '<li> Drivers are not permitted to work if they are showing any symptom of flu or coronavirus- must notify dispatch immediately if already on tour.</li>'+
                      '<li> Upon boarding the coach, the driver must explain to Group Leader the protocols should anyone become ill during the trip.</li>'+
                      '<li> Always wear gloves when handling luggage.</li>'+
                      '<li> Maintain space from passengers when off and on the bus </li>'+
                      '<li> Always wear a mask while driving, when requested by Group Leader </li>'+
                      '<li> Clean high touch areas with higher-grade disinfectant any time passengers are off the bus.</li>'+
                      '<li> Hand sanitizer stations must be located on board and made readily available to group members.</li>'+
                      '<li> No printed material on board (books, magazines, etc.). </li>'+
                      '<li> Bus company will not supply in-vehicle water or beverages.</li>'+
                      '<li> The row of seats directly behind the driver and across from the driver will be unavailable for seating to ensure social distancing.</li>'+
                      '<li> For overnight/ multi-day travel, clean the bus and lock bus doors with no access allowed until agreed upon time.</li></ul>'
                    )
                  );
                  form_gcip_details.add(
                    new Task(
                      OwnerId = UserInfo.getUserId(),
                      RecordTypeId = taskRecordTypeGCIPId,
                      WhatId = formBid.Id,
                      Priority__c = 20,
                      Subject = 'Production/ Passenger Responsibilities',
                       /**Fix By Clay 29 Dec, 2020
                      Description = 
                      '<ul><li>Take temperatures/confirm overall good health prior to travel. </li>'+
                      '<li>Sanitize hands before boarding.</li>'+
                      '<li>Sanitize own luggage handles prior to driver handling luggage</li>'+
                      '<li>Tour is responsible for any water or beverage offerings. This will not be supplied by the bus company.</li>'+
                      '<li>Travel with personal supply of sanitizer, wipes, mask, gloves, etc. </li>'+
                      '<li>No printed material on board (books, magazines, etc.). </li>'+
                      '<li>Maintain space from bus driver when off and on the bus. </li>'+
                      '<li>For overnight/ multi-day travel, make sure all belongings are taken off the bus each night. After the driver disinfects and cleans the bus no access will be allowed until agreed upon time.</li></ul>'
                       )**/
                      Description = 
                      '<ul><li> Take temperatures/confirm overall good health prior to travel. </li>'+
                      '<li> Sanitize hands before boarding.</li>'+
                      '<li> Sanitize own luggage handles prior to driver handling luggage</li>'+
                      '<li> Tour is responsible for any water or beverage offerings. This will not be supplied by the bus company.</li>'+
                      '<li> Travel with personal supply of sanitizer, wipes, mask, gloves, etc. </li>'+
                      '<li> No printed material on board (books, magazines, etc.). </li>'+
                      '<li> Maintain space from bus driver when off and on the bus. </li>'+
                      '<li> For overnight/ multi-day travel, make sure all belongings are taken off the bus each night. After the driver disinfects and cleans the bus no access will be allowed until agreed upon time.</li></ul>'
                    )
                  );
              insert form_gcip_details;
            /** Fix By Clay 28 Dec, 2020
            }else{
              Bid__c b = new Bid__c(id=formBid.Id);
              b.Form_GT_GCIP__c = draft.Name;
              update formBid;**/
            }
            form_gcip_details = [
                SELECT Id, Priority__c, Subject, Description
                FROM Task
                WHERE
                  WhatId = :bidContractId
                  AND RecordTypeId = :taskRecordTypeGCIPId
                ORDER BY Priority__c ASC
              ];
            //Changes as per 175349270
            if(form_gcip_details.size() >0){
              for(Task t : form_gcip_details){
                DashboardController.wrapperTask obj = new DashboardController.wrapperTask();
                obj.Id = t.Id;
                obj.Priority = String.valueOf(t.Priority__c);
                obj.Subject = t.Subject;
                obj.Description = t.Description;
                String str = t.Description.replace('<ul><li>','
 o  ');
                str = str.replace('</li></ul>','');
                str = str.replace('<li>','
 o');
                str = str.replace('</li>','');
                obj.DescriptionOutput = str;
                form_gcip_details_wrapper.add(obj);
              }
            }

        }
        form_attentionList = new List<SelectOption>();                                     //Changes Added as per 175349270    
        Map<String, Contact> contactMap = new Map<String, Contact>();
        for (Contact contact : [
          SELECT Id, FirstName, Name, Title, Phone, Email
          FROM Contact
          WHERE AccountId = :formBid.Vendor__c
        ])
          contactMap.put(contact.Id, contact);
        if (formBid.Vendor__r.ParentId != null)
          for (Contact contact : [
            SELECT Id, FirstName, Name, Title, Phone, Email
            FROM Contact
            WHERE AccountId = :formBid.Vendor__r.ParentId
          ])
            contactMap.put(contact.Id, contact);
            //form_attentionList.add(new SelectOption('', ''));
          for (Contact contact : contactMap.values()){
            form_attentionList.add(new SelectOption(contact.Id, contact.Name));
          }

      switch on bidParentSObject {
        when 'Ground' {
          List<Ground__c> saleGround = [
            SELECT Id, Contracting_Terms__c
            FROM Ground__c
            WHERE
              Production_Ground__c = :formBid.Production__c
              AND RecordType.DeveloperName = 'Sales_GT_Details'
          ];
          switch on formValue {
            when 'Form_Rate_Agreement__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                'Congratulations! You have been selected for the upcoming trip for ' +
                formBid.Production__r.Name +
                '.<br/><br/>Attached is the rate agreement for the group. Please sign and return at your earliest opportunity. <br/><br/>Looking forward to working with you for this production’s trip!. <br/><br/>Thanks,';
              draft.Terms__c = !saleGround.isEmpty()
                ? saleGround[0].Contracting_Terms__c
                : null;
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Primary_Contact_Id__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Trip_Details_Update__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                'Attached you will find updated Trip Details for ' +
                formBid.Production__r.Name +
                '.<br/><br/>Please reply to this email to confirm you have updated these changes or sign and scan the form back to me at your earliest opportunity. If you have any questions, please contact us immediately.<br/><br/>Thanks,';
              draft.Terms__c = '';
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Transportation_Contract__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                'Congratulations! You have been selected for the upcoming trip for ' +
                formBid.Production__r.Name +
                '.<br/><br/>You will receive a separate email soon from Conga Sign which is the contract for the group. Please sign and submit today so we can forward to the client. If you absolutely need to use your company contract, then please include all items in the attached contract into your own contract. ‘Road Rebel’ and their employees should not appear on your agreement.<br/><br/>Please sign and submit only one contract to me as soon as possible. Looking forward to working with you for this production’s trip!<br/><br/><br/>Thanks,';
              draft.Terms__c = (!saleGround.isEmpty()
                ? saleGround[0].Contracting_Terms__c
                : ''); //'<ul><li>Driver(s) must assist with luggage.</li><li>Driver(s) will be on time, drive safely and only use cell phones in emergencies.</li><li>Driver(s) name and cell will be provided prior to travel.</li><li>Driver(s) are responsible for having directions to destination.</li><li>Bus company will not sub-contract coaches.</li><li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from Tour Management should be adhered to. Weather or roadway conditions, infringement on D.O.T regulations or the intervention of any governmental body are of exception. Road Rebel should be contacted immediately should any of the events listed occur.</li></ul>';
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Primary_Contact_Id__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Contract_to_Client__c' {
              draft.Subject__c =
                'Contract to Sign - ' +
                (String.isNotEmpty(formBid.Vendor__c)
                  ? formBid.Vendor__r.Name + ' - '
                  : '') +
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                'The following contract is ready and awaiting your signature. You will receive the contract shortly via Conga Sign. Please sign and email back electronically.<br/><br/><ul><li>' +
                vendor.Name +
                ' – ' +
                (String.isNotEmpty(vendor.City__c)
                  ? vendor.City__r.Name + ' – '
                  : '') +
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' – ' +
                Datetime.newInstance(bidEndDate, Time.newInstance(0, 0, 0, 0))
                  .format('dd MMM yyyy') +
                ' (' +
                bidParentCode +
                ')</li></ul><br/>Please review, sign and include any missing spot times or updates needed. Please call me with any questions or updates!<br/><br/><br/>Thank you,';
              draft.Production_Assoc_Contact_Id__c = contractSignerContact !=
                null
                ? contractSignerContact.Id
                : null;
            }
            when 'Form_Counter_Needed__c' {
              draft.Subject__c =
                'Counter Needed - ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached you will find a signed contract for the upcoming trip for ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                '.</p>';
              draft.Body__c += '<p>Please initial next to any updates or simply reply to this email to confirm you have updated your system.</p>';
              draft.Body__c += '<p>If you have any questions, please contact us immediately.</p>';
              draft.Body__c += '<p>Thanks,</p>';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Final_Contract__c' {
              draft.Subject__c =
                'Final Contract - ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached you will find a final contract for the upcoming trip for ' +
                formBid.Production__r.Name +
                ' - ' +
                Datetime.newInstance(bidStartDate, Time.newInstance(0, 0, 0, 0))
                  .format('dd MMM yyyy') +
                ', ' +
                formBid.GT__r.Description__c +
                '. Please retain for your records.</p>';
              draft.Body__c += '<p>If you have any questions, please contact us immediately.</p>';
              draft.Body__c += '<p>Thanks,</p>';
              draft.Production_Assoc_Contact_Id__c = contractSignerContact !=
                null
                ? contractSignerContact.Id
                : null;
            }
            when 'Form_Credit_Card_Change__c' {
              draft.Subject__c =
                '*Important* Credit Card Changes for - ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached is the new credit card for the upcoming trip for ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                '.</p><p>Delete the old credit card from your records and use this credit card as per the billing instructions on your contract.</p><p>Please reply to this email to confirm you have received this change and have updated your system accordingly.</p><p>Thanks,</p>';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Email_Confirmation__c' {
              draft.Subject__c =
                (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' Travel Confirmations for ' +
                formBid.Production__r.Name;
              draft.Body__c = 'Please review the attached confirmations for your upcoming travel.<br/><br/>All details have been confirmed with the vendors and your contact information has been provided to them. Please don’t hesitate to contact their dispatch if there are any questions or last minute changes that they can update directly.<br/><br/>Bus driver assignment is based on information given at the time of confirmation call and is subject to change. For up-to-date driver information, we recommend that you call dispatch at the number listed the day prior/morning of trip.<br/><br/>Thanks,';
            }
            when 'Form_Cancellation_Letter__c' {
              draft.Subject__c =
                'Trip ' +
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                ' (' +
                formBid.GT__r.Name +
                ')';
              draft.Body__c =
                'Please cancel the trip for ' +
                formBid.Production__r.Name +
                (formBid.GT__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.GT__r.Description__c)
                  ? ', ' + formBid.GT__r.Description__c
                  : '') +
                '.<br/><br/>Thank you for helping me with their proposed needs. We will be sure to keep you in mind for future trips in your area.<br/><br/>Please reply to this email to confirm you have cancelled the above trip.<br/><br/>If you have any further questions, feel free to contact us.<br/><br/>Thanks,';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Create_GCIP__c' {        //Changes Added as per 17534927
              /**Fix By Clay 31 Dec, 2020
              draft.Subject__c = '*Response Needed* Ground Transportation Procedures – Trip ID: '+formBid.GT__r.Name +' which is ' + formBid.Production__r.Name + ' production, and the dated of ' +
              (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '');**/
              draft.Subject__c = '*Response Needed* Ground Transportation Procedures – ' + formBid.Production__r.Name + ' - ' +
              (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') + ' - ' + formBid.GT__r.Name;
              draft.Body__c = 'Below are the driver and passenger cleanliness responsibilities to be followed for ' + formBid.Production__r.Name + 
              ' traveling with you '+
              (formBid.GT__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.GT__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.GT__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '')+'.'+
                  '

'+
                  'Please reply to this email to confirm you are agreeing to abide by all driver responsibilities and that you are aware of the '+
                  'passenger responsibilities. Please include a copy of your company COVID-19 guidelines

'+
                  'If you cannot agree to a procedure, please notify Road Rebel immediately.';

            }

          }
        }
        when 'Freight' {
          switch on formValue {
            when 'Form_Rate_Agreement__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.Freight__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                'Congratulations! You have been selected for the upcoming trip for ' +
                formBid.Production__r.Name +
                '.<br/><br/>Attached is the rate agreement for the group. Please sign and return at your earliest opportunity. <br/><br/>Looking forward to working with you for this production’s trip!. <br/><br/>Thanks,';
              draft.Terms__c = '';
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Primary_Contact_Id__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Trip_Details_Update__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.Freight__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                'Attached you will find updated Trip Details for ' +
                formBid.Production__r.Name +
                '.<br/><br/>Please reply to this email to confirm you have updated these changes or sign and scan the form back to me at your earliest opportunity. If you have any questions, please contact us immediately.<br/><br/>Thanks,';
              draft.Terms__c = '';
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Transportation_Contract__c' {
              draft.Subject__c =
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                ' - ' +
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' - ' +
                (formBid.Freight__r.End_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.End_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                'Congratulations! You have been selected for the upcoming trip for ' +
                formBid.Production__r.Name +
                '.<br/><br/>You will receive a separate email soon from Conga Sign which is the contract for the group. Please sign and submit today so we can forward to the client. If you absolutely need to use your company contract, then please include all items in the attached contract into your own contract. ‘Road Rebel’ and their employees should not appear on your agreement.<br/><br/>Please sign and submit only one contract to me as soon as possible. Looking forward to working with you for this production’s trip!<br/><br/><br/>Thanks,';
              draft.Terms__c = '<ul><li>Driver(s) must assist with luggage.</li><li>Driver(s) will be on time, drive safely and only use cell phones in emergencies.</li><li>Driver(s) name and cell will be provided prior to travel.</li><li>Driver(s) are responsible for having directions to destination.</li><li>Bus company will not sub-contract coaches.</li><li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from Tour Management should be adhered to. Weather or roadway conditions, infringement on D.O.T regulations or the intervention of any governmental body are of exception. Road Rebel should be contacted immediately should any of the events listed occur.</li></ul>';
              draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Payment_policy__c
                : null;
              draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c)
                ? bid.Vendor__r.Cancellation_Policy__c
                : null;
              draft.Primary_Contact_Id__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Contract_to_Client__c' {
              draft.Subject__c =
                'Contract to Sign - ' +
                (String.isNotEmpty(formBid.Vendor__c)
                  ? formBid.Vendor__r.Name + ' - '
                  : '') +
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                'The following contract is ready and awaiting your signature. You will receive the contract shortly via Conga Sign. Please sign and email back electronically.<br/><br/><ul><li>' +
                vendor.Name +
                ' – ' +
                (String.isNotEmpty(vendor.City__c)
                  ? vendor.City__r.Name + ' – '
                  : '') +
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' – ' +
                Datetime.newInstance(bidEndDate, Time.newInstance(0, 0, 0, 0))
                  .format('dd MMM yyyy') +
                ' (' +
                bidParentCode +
                ')</li></ul><br/>Please review, sign and include any missing spot times or updates needed. Please call me with any questions or updates!<br/><br/><br/>Thank you,';
              draft.Production_Assoc_Contact_Id__c = contractSignerContact !=
                null
                ? contractSignerContact.Id
                : null;
            }
            when 'Form_Counter_Needed__c' {
              draft.Subject__c =
                'Counter Needed - ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached you will find a signed contract for the upcoming trip for ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                '.</p>';
              draft.Body__c += '<p>Please initial next to any updates or simply reply to this email to confirm you have updated your system.</p>';
              draft.Body__c += '<p>If you have any questions, please contact us immediately.</p>';
              draft.Body__c += '<p>Thanks,</p>';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Final_Contract__c' {
              draft.Subject__c =
                'Final Contract - ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached you will find a final contract for the upcoming trip for ' +
                formBid.Production__r.Name +
                ' - ' +
                Datetime.newInstance(bidStartDate, Time.newInstance(0, 0, 0, 0))
                  .format('dd MMM yyyy') +
                ', ' +
                formBid.Freight__r.Description__c +
                '. Please retain for your records.</p>';
              draft.Body__c += '<p>If you have any questions, please contact us immediately.</p>';
              draft.Body__c += '<p>Thanks,</p>';
              draft.Production_Assoc_Contact_Id__c = contractSignerContact !=
                null
                ? contractSignerContact.Id
                : null;
            }
            when 'Form_Credit_Card_Change__c' {
              draft.Subject__c =
                '*Important* Credit Card Changes for - ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                '<p>Attached is the new credit card for the upcoming trip for ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                '.</p><p>Delete the old credit card from your records and use this credit card as per the billing instructions on your contract.</p><p>Please reply to this email to confirm you have received this change and have updated your system accordingly.</p><p>Thanks,</p>';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
            when 'Form_Email_Confirmation__c' {
              draft.Subject__c =
                (formBid.Freight__r.Start_Date__c != null
                  ? Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                ' Travel Confirmations for ' +
                formBid.Production__r.Name;
              draft.Body__c = 'Please review the attached confirmations for your upcoming travel.<br/><br/>All details have been confirmed with the vendors and your contact information has been provided to them. Please don’t hesitate to contact their dispatch if there are any questions or last minute changes that they can update directly.<br/><br/>Bus driver assignment is based on information given at the time of confirmation call and is subject to change. For up-to-date driver information, we recommend that you call dispatch at the number listed the day prior/morning of trip.<br/><br/>Thanks,';
            }
            when 'Form_Cancellation_Letter__c' {
              draft.Subject__c =
                'Trip ' +
                (String.isNotBlank(formLabel) ? formLabel + ' - ' : '') +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                ' (' +
                formBid.Freight__r.Name +
                ')';
              draft.Body__c =
                'Please cancel the trip for ' +
                formBid.Production__r.Name +
                (formBid.Freight__r.Start_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Freight__r.Start_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (String.isNotBlank(formBid.Freight__r.Description__c)
                  ? ', ' + formBid.Freight__r.Description__c
                  : '') +
                '.<br/><br/>Thank you for helping me with their proposed needs. We will be sure to keep you in mind for future trips in your area.<br/><br/>Please reply to this email to confirm you have cancelled the above trip.<br/><br/>If you have any further questions, feel free to contact us.<br/><br/>Thanks,';
              draft.Attention__c = contactPrimaryBid != null
                ? contactPrimaryBid.Id
                : null;
            }
          }
        }
        when 'Air' {
          getAirInformationByBid();
          switch on formValue {
            when 'Form_Deposit_Due__c' {
              draft.Subject__c =
                'Air Deposit_Due ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '') +
                ', Deposit Due {ClientDueDate}';
              draft.Body__c =
                'This is to remind you that your deposit of' +
                (symbolsMap.containsKey(formBid.Deposit_Amount_Currency__c)
                  ? ' ' + symbolsMap.get(formBid.Deposit_Amount_Currency__c)
                  : '') +
                (formBid.Deposit_Amount_per_seat__c != null
                  ? String.valueOf(formBid.Deposit_Amount_per_seat__c)
                  : '') +
                ' per person is Due on {ClientDueDate} for the' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities
                  : '') +
                ' trip. If deposit is not received by this date the reservation will auto cancel.<br/><br/>Please send approval to use the credit card on file or fill out the attached form and send it back for payment.<br/><br/>Let me know if you have any questions!<br/>';
              draft.Attention__c = clientContact.Id;
            }
            when 'Form_Utilization__c' {
              Decimal itinerarySeats = 0;
              for (Revenue__c rate : [
                SELECT id, of_seats__c
                FROM Revenue__c
                WHERE
                  Bid__c = :formBid.id
                  AND RecordType.DeveloperName = 'Air_Rate_Commission'
                  AND of_seats__c != NULL
              ])
                itinerarySeats += rate.of_seats__c;
              draft.Subject__c =
                'Utilization ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '') +
                ', Utilization Due {ClientDueDate}';
              draft.Body__c =
                'This is to remind you that the last day to cancel/reduce without penalty is on {ClientDueDate} for the' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities + ' trip'
                  : '') +
                ' with' +
                (String.isNotBlank(formBid.Vendor__r.Name)
                  ? ' ' + formBid.Vendor__r.Name
                  : '') +
                '. Please let us know if you’d like to make any changes to your passenger count by {ClientDueDate}.' +
                '<br/><ul><li>After that date we are locked into' +
                (formBid.Utilization_Percentage__c != null
                  ? ' ' +
                    String.valueOf(formBid.Utilization_Percentage__c.round())
                  : '') +
                '% of seats.</li><li>Should you fall below the required' +
                (formBid.Utilization_Percentage__c != null
                  ? ' ' +
                    String.valueOf(formBid.Utilization_Percentage__c.round())
                  : '') +
                '%, ' +
                (String.isNotBlank(formBid.Vendor__r.Name)
                  ? ' ' + formBid.Vendor__r.Name
                  : '') +
                ' charges a fee of' +
                (symbolsMap.containsKey(formBid.Utilization_Penalty_Currency__c)
                  ? ' ' +
                    symbolsMap.get(formBid.Utilization_Penalty_Currency__c)
                  : '') +
                (formBid.Utilization_Penalty_per_seat__c != null
                  ? ' ' +
                    String.valueOf(formBid.Utilization_Penalty_per_seat__c)
                  : '') +
                ' for each seat that you fall below required percentage.</li><li>We are currently holding ' +
                String.valueOf(itinerarySeats) +
                ' seats.</li></ul>Let me know if you have any questions!<br/><br/>Thank you,';
              draft.Attention__c = clientContact.Id;
            }
            when 'Form_Names_Final_Payment__c' {
              draft.Subject__c =
                'Names & Final Payment ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '') +
                ', Names & Ticketing Due {ClientDueDate}';
              draft.Body__c =
                'This is to remind you that the passenger name list and payment is Due on {ClientDueDate} for the' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '') +
                ', Team trip.<br/><br/>The airlines will only accept names being submitted on the attached template. Please enter names (as they appear on their government issued ID), date of birth and gender per the example listed. If not entered correctly, the template will be rejected.  Airlines will deny boarding if names do not match your legal document at airport check in.<br/><br/>Let me know if you have any questions!<br/>';
              draft.Attention__c = clientContact.Id;
            }
            when 'Form_Final_Choice__c' {
              draft.Subject__c =
                'Final Choice ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '');
              draft.Body__c =
                'Flights for the group trip on' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities
                  : '') +
                ' have been confirmed. Please review the attached document. It contains all applicable due dates and the group policies for the trip.<br/><br/>We’ll be sure to send a reminder email prior to each due date so you know they are approaching.<br/><br/>Let me know if you have any questions!<br/>';
              draft.Production_Assoc_Contact_Id__c = clientContact.Id;
            }
            when 'Form_Ticketed_Confirmation__c' {
              draft.Subject__c =
                'Ticketed Confirmation ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '');
              draft.Body__c =
                'Attached is your ticketed confirmation for the group trip on' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities + '.'
                  : '') +
                '<br/><br/>Seat configuration of the aircraft' +
                (String.isNotBlank(firstBidItinerarySegment.Equip_Type__c)
                  ? ' ' + firstBidItinerarySegment.Equip_Type__c
                  : '') +
                ' is the layout of: ABC DEF. Charges associated with the trip are on the attached confirmation. We’ll be calling a few days prior to travel to reconfirm the flights.<br/><br/>Let me know if you have any questions!<br/>';
              draft.Production_Assoc_Contact_Id__c = clientContact.Id;
            }
            when 'Form_Final_Air_Confirmation__c' {
              draft.Subject__c =
                'Final Air Confirmation ' +
                formBid.Production__r.Name +
                (formBid.Air__r.Departure_Date__c != null
                  ? ', ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ', ' + airSegmentCities
                  : '') +
                (String.isNotEmpty(formBid.Air__r.Group_Type__c)
                  ? ', ' + formBid.Air__r.Group_Type__c
                  : '');
              draft.Body__c =
                'We have reconfirmed your group flight on' +
                (formBid.Air__r.Departure_Date__c != null
                  ? ' ' +
                    Datetime.newInstance(
                        formBid.Air__r.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yyyy')
                  : '') +
                (formBid.Air__r.Return_Date__c != null
                  ? ' - ' +
                    Datetime.newInstance(
                        formBid.Air__r.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('dd MMMMM yy')
                  : '') +
                (String.isNotBlank(airSegmentCities)
                  ? ' ' + airSegmentCities + '.'
                  : '') +
                '<br/><br/>Your' +
                (String.isNotBlank(formBid.Vendor__r.Name)
                  ? ' ' + formBid.Vendor__r.Name
                  : '') +
                ' confirmation is attached for your review.<br/><br/>If there is anything you might need, please feel free to contact me.<br/>';
              draft.Production_Assoc_Contact_Id__c = clientContact.Id;
            }
          }
        }
      }
      if (String.isNotBlank(draft.Subject__c)) {
        insert draft;
        draft = [
          SELECT
            Id,
            Name,
            Salutation__c,
            Attention__c,
            Primary_Contact_Id__c,
            Production_Assoc_Contact_Id__c,
            CC__c,
            Subject__C,
            Date__c,
            BCC__c,
            Body__c,
            Terms__c,
            CreatedById,
            CreatedBy.Name,
            CreatedDate,
            LastModifiedBy.Name,
            LastModifiedDate,
            Payment_Policy__c,
            Cancellation_Policy__c,
            Production_Assoc_Type__c,
            Credit_Card_Id__c
          FROM Draft__c
          WHERE Id = :draft.Id
        ];
        //Fix By Clay 29 Dec, 2020
        if(bidParentSObject == 'Ground' && String.isBlank(formBid.Form_GT_GCIP__c)) {
            Bid__c b = new Bid__c(id=formBid.Id);
            b.Form_GT_GCIP__c = draft.Name;
            update b;
            formBid.Form_GT_GCIP__c = draft.Name;
        }
          
        switch on formValue {
          when 'Form_Rate_Agreement__c' {
            formBid.Form_Rate_Agreement__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Rate_Agreement__c = draft.Name
            );
          }
          when 'Form_Contract_to_Client__c' {
            formBid.Form_Contract_to_Client__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Contract_to_Client__c = draft.Name
            );
          }
          when 'Form_Counter_Needed__c' {
            formBid.Form_Counter_Needed__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Counter_Needed__c = draft.Name
            );
          }
          when 'Form_Final_Contract__c' {
            formBid.Form_Final_Contract__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Final_Contract__c = draft.Name
            );
          }
          when 'Form_Transportation_Contract__c' {
            formBid.Form_Transportation_Contract__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Transportation_Contract__c = draft.Name
            );
          }
          when 'Form_Trip_Details_Update__c' {
            formBid.Form_Trip_Details_Update__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Trip_Details_Update__c = draft.Name
            );
          }
          when 'Form_Credit_Card_Change__c' {
            formBid.Form_Credit_Card_Change__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Credit_Card_Change__c = draft.Name
            );
          }
          when 'Form_Email_Confirmation__c' {
            formBid.Form_Email_Confirmation__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Email_Confirmation__c = draft.Name
            );
          }
          /*
          when 'Form_Create_GCIP__c' {                   //Changes Added as per 175349270
            formBid.Form_Create_GCIP__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Create_GCIP__c = draft.Name
            );
          }
          */
          when 'Form_Cancellation_Letter__c' {
            formBid.Form_Cancellation_Letter__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Cancellation_Letter__c = draft.Name
            );
          }
          when 'Form_Deposit_Due__c' {
            formBid.Form_Deposit_Due__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Deposit_Due__c = draft.Name
            );
          }
          when 'Form_Utilization__c' {
            formBid.Form_Utilization__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Utilization__c = draft.Name
            );
          }
          when 'Form_Names_Final_Payment__c' {
            formBid.Form_Names_Final_Payment__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Names_Final_Payment__c = draft.Name
            );
          }
          when 'Form_Final_Choice__c' {
            formBid.Form_Final_Choice__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Final_Choice__c = draft.Name
            );
          }
          when 'Form_Ticketed_Confirmation__c' {
            formBid.Form_Ticketed_Confirmation__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Ticketed_Confirmation__c = draft.Name
            );
          }
          when 'Form_Final_Air_Confirmation__c' {
            formBid.Form_Final_Air_Confirmation__c = draft.Name;
            update new Bid__c(
              Id = formBid.Id,
              Form_Final_Air_Confirmation__c = draft.Name
            );
          }
        }
      }
    }
    if (
      formValue != 'Form_Credit_Card_Change__c' &&
      formValue != 'Form_Cancellation_Letter__c'
    ) {
      if (bidParentSObject == 'Ground') {
        bidAgreementSubTrips = [
          SELECT
            id,
            Trip_Order__c,
            Sub_Trip_Type__c,
            Description__c,
            Sub_Trip_Notes__c,
            (
              SELECT
                id,
                Line__c,
                Vehicle_Ref__c,
                Start_Date__c,
                Start_Date_Time__c,
                End_Date__c,
                End_Date_Time__c,
                Travel_Type__c,
                Group_Type__c,
                Location_Pick_up__c,
                Location_Type__c,
                Location_Details__c,
                Location_Drop_off__c,
                Location_Drop_Off_Type__c,
                Location_Details_Drop_Off__c,
                Airline_Info_Special_Notes__c
              FROM GTTravels__r
              ORDER BY Line__c
            )
          FROM Ground__c
          WHERE
            Bid_Sub_Trip__c = :formBid.Id
            AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'
          ORDER BY Trip_Order__c, Line__c
        ];
        bidAgreementVehicles = [
          SELECT
            id,
            Name,
            Vehicle_Ref__c,
            Vehicle_Type__c,
            Capacity__c,
            Make_Model__c,
            Year__c,
            Amenities__c,
            Other_Amenities__c
          FROM Ground__c
          WHERE
            Bid__c = :formBid.Id
            AND RecordType.DeveloperName = 'Vehicle_Type'
        ];
      } else if (bidParentSObject == 'Freight') {
        bidAgreementSubTrips = [
          SELECT
            id,
            Trip_Order__c,
            Sub_Trip_Type__c,
            Description__c,
            Sub_Trip_Notes__c,
            (
              SELECT
                id,
                Line__c,
                Equipment__c,
                Start_Date__c,
                Start_Date_Time__c,
                End_Date__c,
                End_Date_Time__c,
                Travel_Type__c,
                Group_Type__c,
                Location_Pick_up__c,
                Location_Type__c,
                Location_Details__c,
                Location_Drop_off__c,
                Location_Drop_Off_Type__c,
                Location_Details_Drop_Off__c,
                Airline_Info_Special_Notes__c
              FROM FreightEquipments__r
              ORDER BY Line__c
            )
          FROM Freight__c
          WHERE
            Bid_Sub_Trip__c = :formBid.Id
            AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'
          ORDER BY Trip_Order__c, Line__c
        ];
        bidAgreementVehicles = [
          SELECT
            id,
            Name,
            Equipment__c,
            Vehicle_Type__c,
            Capacity__c,
            Make__c,
            Model__c,
            Make_Model__c,
            Year__c,
            Freight_Truck_Sq_Ft__c,
            Amenities__c,
            Other_Amenities__c,
            Equipment_requested__c
          FROM Freight__c
          WHERE
            Bid__c = :formBid.Id
            AND RecordType.DeveloperName = 'Vehicle_Type'
        ];
      }
      bidAgreementConcessions = [
        SELECT id, Concession_Provided__c
        FROM Concessions__c
        WHERE Bid__c = :formBid.Id AND Concession_Type__c = :dashboard
      ];
      if (formValue == 'Form_Email_Confirmation__c')
        searchContactData();
      /**
       *  @Conga: Update for Conga.
       */
      Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
      for (APXTConga4__Conga_Merge_Query__c congaQuery : [
        SELECT Id, APXTConga4__Name__c
        FROM APXTConga4__Conga_Merge_Query__c
        WHERE
          APXTConga4__Name__c IN :(bidParentSObject == 'Ground'
            ? new List<String>{
                'GT - BidById',
                'GT - SubTripsByBidId',
                'GT - SubTripsByGCQId',
                'GT - GCQById',
                'GT - ContactById',
                'GT - ClientContactById',
                'GT - ProductionAssociationsByOppId',
                'GT - UserById'
              }
            : bidParentSObject == 'Freight'
                ? new List<String>{
                    'Freight - BidById',
                    'Freight - SubTripsByBidId',
                    'Freight - SubTripsByFCQId',
                    'Freight - FCQById',
                    'Freight - ContactById',
                    'Freight - ClientContactById',
                    'Freight - ProductionAssociationsByOppId',
                    'Freight - UserById'
                  }
                : bidParentSObject == 'Air'
                    ? new List<String>{ 'Air - BidById', 'Air - GCQById' }
                    : new List<String>())
      ])
        congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
      bidAgreement_congaQueriesJson = JSON.serialize(congaQueriesMap);
      List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [
        SELECT Id
        FROM APXTConga4__Conga_Email_Template__c
        WHERE
          APXTConga4__Name__c = :(dashboard +
          ' - ' +
          (formLabel == 'Final Air Confirmation'
            ? 'Air Confirmation'
            : formLabel))
      ];
      bidAgreement_congaEmailTemplateId = !congaEmailTemplates.isEmpty()
        ? congaEmailTemplates[0].id
        : null;
      Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
      for (APXTConga4__Conga_Template__c congaTemplate : [
        SELECT Id, APXTConga4__Name__c
        FROM APXTConga4__Conga_Template__c
        WHERE
          APXTConga4__Name__c IN (
            :(dashboard +
            ' - ' +
            (formLabel == 'Final Air Confirmation'
              ? 'Air Confirmation'
              : formLabel)),
            :(dashboard +
            ' - ' +
            formLabel +
            ' Sign')
          )
      ])
        congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
      bidAgreement_congaTemplateId = congaTemplatesMap.get(
          dashboard +
          ' - ' +
          (formLabel == 'Final Air Confirmation'
            ? 'Air Confirmation'
            : formLabel)
        ) != null
        ? congaTemplatesMap.get(
              dashboard +
              ' - ' +
              (formLabel == 'Final Air Confirmation'
                ? 'Air Confirmation'
                : formLabel)
            )
            .id
        : null;
      bidAgreement_congaSignTemplateId = congaTemplatesMap.get(
          dashboard +
          ' - ' +
          formLabel +
          ' Sign'
        ) != null
        ? congaTemplatesMap.get(dashboard + ' - ' + formLabel + ' Sign').id
        : null;
      /**
       *  @/Conga
       */
    }
    if (isNew) {
      for (Dashboard_Tab_Contract_Forms.FormWrapper formButton : formList1)
        if (formButton.value.equals(formValue))
          formButton.draftCode = draft.Name;
      for (Dashboard_Tab_Contract_Forms.FormWrapper formButton : formList2)
        if (formButton.value.equals(formValue))
          formButton.draftCode = draft.Name;
    }
    if (String.isNotBlank(draft.Primary_Contact_Id__c))
      changeBidAgreementContactPrimary();
    else if (
      String.isNotBlank(draft.Production_Assoc_Contact_Id__c) &&
      String.isBlank(draft.Production_Assoc_Type__c)
    )
      changeBidAgreementProductionAssociationContact();
    else if (String.isNotBlank(draft.Attention__c))
      changeBidAgreementAttentionContact();
    isBidAgreementRendered = true;
  }

//Changes as per 175349270
public static User verifyEmailUser(
    String userId,
    String productionId,
    String stayId
  ) {
    User userActual = new User();
    Map<String, User> associationsMap = new Map<String, User>();
    Set<Id> userIds = new Set<Id>();
    for (Production_Associations__c pa : [
      SELECT
        Id,
        User__c,
        User__r.Name,
        User__r.Email,
        User__r.Phone,
        Team_Roles__c,
        Production_Opp__c,
        Housing__c
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :productionId
        AND RecordType.DeveloperName = 'Production_Coordinators'
        AND User__c != NULL
        AND Team_Roles__c != NULL
    ]) {
      system.debug ('pa :: ' + pa);
      if (pa.Team_Roles__c != null) {
        for (String teamrole : pa.Team_Roles__c.split(';')) {
          if (
            pa.Production_Opp__c != null &&
            teamrole.toLowerCase() != 'housing back-end coordinator'
          ) {
            associationsMap.put(
              teamrole.toLowerCase(),
              new User(Id = pa.User__c)
            );
            userIds.add(pa.User__c);
          }
        }
      }
    }
    List<Housing__c> housingList = [
      SELECT Id, Back_end_Coordinator__c
      FROM Housing__c
      WHERE Id = :stayId
    ];
    if (!housingList.isEmpty()) {
      associationsMap.put(
        'housing back-end coordinator',
        new User(Id = housingList[0].Back_end_Coordinator__c)
      );
      userIds.add(housingList[0].Back_end_Coordinator__c);
    }
    system.debug ('associations Map: ' + associationsMap);
    if (!associationsMap.isEmpty()) {
      for (User us : [
        SELECT Id, Name, Email, Phone
        FROM User
        WHERE Id IN :userIds
      ]) {
        for (String key : associationsMap.keySet()) {
          if (associationsMap.get(key).Id == us.Id)
            associationsMap.put(key, us);
        }
      }
      if (
        associationsMap.get('primary housing coordinator') != null &&
        associationsMap.get('primary housing coordinator').Id == userId
      )
        userActual = associationsMap.get('primary housing coordinator');
      else if (
        associationsMap.get('housing back-end coordinator') != null &&
        associationsMap.get('housing back-end coordinator').Id != null
      )
        userActual = associationsMap.get('housing back-end coordinator');
      else if (associationsMap.get('primary housing coordinator') != null)
        userActual = associationsMap.get('primary housing coordinator');
    } 
    system.debug('userActual :: ' + userActual);
    return userActual;
  }
  public static String sendEmail(
    String toList,
    String ccList,
    String bccList,
    String subject,
    String body,
    String attachs,
    String oppid,
    String stayid
  ) {
    try {
      //TO
      Set<String> toAddress = new Set<String>();
      for (String k : toList.split(',')) {
        if (k.trim() != '')
          toAddress.add(k.trim());
      }
      //CC
      Set<String> ccAddress = new Set<String>();
      for (String k : ccList.split(',')) {
        if (k.trim() != '')
          ccAddress.add(k.trim());
      }
      //BCC
      Set<String> bccAddress = new Set<String>();
      for (String k : bccList.split(',')) {
        if (k.trim() != '')
          bccAddress.add(k.trim());
      }

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: oppid AND User__c <> NULL AND Team_Roles__c includes ('Primary Housing Coordinator')];
      User userActual = verifyEmailUser(UserInfo.getUserId(), oppid, stayid);

      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
      if (userActual != null && userActual.Email != null)
        mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
      mail.setToAddresses(new List<String>(toAddress));
      if (ccAddress.size() > 0)
        mail.setCcAddresses(new List<String>(ccAddress));
      if (bccAddress.size() > 0)
        mail.setBccAddresses(new List<String>(bccAddress));
      mail.setSubject(subject);
      mail.setHtmlBody(body);

      if (attachs != null) {
        Set<String> attachIds = new Set<String>();
        for (String att : attachs.split(',')) {
          if (att.trim() != '')
            attachIds.add(att.trim());
        }
        //Attachment
        Set<String> versionIds = new Set<String>();
        for (ContentDocument cd : [
          SELECT Id, LatestPublishedVersionId
          FROM ContentDocument
          WHERE Id IN :attachIds
        ])
          versionIds.add(cd.LatestPublishedVersionId);
        List<ContentVersion> contentVersions = [
          SELECT Id, ContentDocumentId, Title, PathOnClient, VersionData
          FROM ContentVersion
          WHERE Id IN :versionIds
          ORDER BY Id ASC
        ];
        List<Messaging.Emailfileattachment> fileAttachments = new List<Messaging.Emailfileattachment>();
        if (contentVersions.size() > 0) {
          Messaging.Emailfileattachment efa;
          for (ContentVersion cv : contentVersions) {
            efa = new Messaging.Emailfileattachment();
            efa.setFileName(
              cv.PathOnClient.subString(1, cv.PathOnClient.length())
            );
            efa.setBody(cv.VersionData);
            fileAttachments.add(efa);
          }
        }
        if (fileAttachments.size() > 0)
          mail.setFileAttachments(fileAttachments);
      }
      system.debug(mail.getToAddresses());
      system.debug(mail.getCcAddresses());
      system.debug(mail.getBccAddresses());
      myEmails.add(mail);
      Messaging.SendEmailResult[] mailResult = Messaging.sendEmail(myEmails);
      if (!mailResult[0].isSuccess()) {
        system.debug(mailResult[0].getErrors()[0].getMessage());
        return mailResult[0].getErrors()[0].getMessage();
      }
    } catch (System.EmailException e) {
      system.debug(e.getMessage());
      return e.getMessage();
    }
    return '';
  }
  public void sendEmailFormWithAttachs() {

    // CHECK CC BCC
    //saveForm();
    try {
      List<Task> traceTasks = new List<Task>();
        form_body += '<ul>';
        for (Task task : form_gcip_details)
          form_body += '<li>' + task.Description + '</li>';
        form_body += '</ul>';
      if (String.isNotBlank(bidAgreementAttentionContact_Salutation))
        form_body = '<p>' + bidAgreementAttentionContact_Salutation + '</p>' + form_body;
      if (String.isNotBlank(form_closing))
        form_body +=
          '<p>' +
          form_closing.replaceAll('
|
|', '</p><p>') +
          '</p>';

      // CHECK CC
      emailMessage = sendEmail(
        form_to,
        form_cc,
        form_bcc,
        form_subject,
        form_body,
        emailAttachs,
        formBid.Production__c,
        formBid.Housing__c
      );
      Bid__c bid;
      bid = new Bid__c(
        id = formBid.id,
        GCIP_Last_Send_Date__c = Datetime.now()
      );
      update bid;
      formBid.GCIP_Last_Send_Date__c = bid.GCIP_Last_Send_Date__c;
      /*
      if (
        contractTasksMap.containsKey('Create GCIP') &&
        contractTasksMap.get('Create GCIP').ActivityDate != null
      ) {
        traceTasks.add(
          new Task(
            Id = contractTasksMap.get('Create GCIP').Id,
            Status = 'Completed',
            ActivityDate = null
          )
        );
        JournalCreation.insertJournal(
          new List<JournalCreation.JournalEntry>{
            new JournalCreation.JournalEntry(
              'bid',
              bidData.Id,
              bidJournalRT,
              'Created GCIP'
            )
          }
        );
      }
      if (contractTasksMap.containsKey('Awaiting GCIP')) {
        traceTasks.add(
          new Task(
            Id = contractTasksMap.get('Awaiting GCIP').Id,
            Status = 'Open',
            ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 2)
          )
        );
        JournalCreation.insertJournal(
          new List<JournalCreation.JournalEntry>{
            new JournalCreation.JournalEntry(
              'bid',
              bidData.Id,
              bidJournalRT,
              'Awaiting GCIP: Due Date is change to ' +
              (Datetime.newInstance(
                  BusinessDate.AddBusinessDays(Date.today(), 2),
                  Time.newInstance(0, 0, 0, 0)
                ))
                .format('dd-MMM-YYYY')
            )
          }
        );
      }
      JournalCreation.insertJournal(
        new List<JournalCreation.JournalEntry>{
          new JournalCreation.JournalEntry(
            'bid',
            bidData.Id,
            bidJournalRT,
            'GCIP has been sent to: ' +
            form_attentionContact.Name +
            ' at ' +
            form_attentionContact.Email
          )
        }
      );
      
      if (!traceTasks.isEmpty()) {
        update traceTasks;
        //bidContractedStatus();
      }
      //getBidJournals();
      */
    } catch (DMLException e) {
      emailMessage = e.getMessage();
      System.debug('Send Email Exception: '+emailMessage);
    }
  }

  public List<SelectOption> getContactsBidsByVendor() {
    Map<String, Contact> contactMap = new Map<String, Contact>();
    for (Contact contact : [
      SELECT Id, FirstName, Name, Title, Phone, Email
      FROM Contact
      WHERE AccountId = :formBid.Vendor__c
    ])
      contactMap.put(contact.Id, contact);
    if (formBid.Vendor__r.ParentId != null)
      for (Contact contact : [
        SELECT Id, FirstName, Name, Title, Phone, Email
        FROM Contact
        WHERE AccountId = :formBid.Vendor__r.ParentId
      ])
        contactMap.put(contact.Id, contact);
    bidAgreementPrimaryContact = contactMap.get(draft.Primary_Contact_Id__c) !=
      null
      ? contactMap.get(draft.Primary_Contact_Id__c)
      : new Contact();
    bidAgreementAttentionContact = contactMap.get(draft.Attention__c) != null
      ? contactMap.get(draft.Attention__c)
      : new Contact();
    List<SelectOption> contactsBidsByVendor = new List<SelectOption>();
    contactsBidsByVendor.add(new SelectOption('', ''));
    for (Contact contact : contactMap.values())
      contactsBidsByVendor.add(new SelectOption(contact.Id, contact.Name));
    return contactsBidsByVendor;
  }
  public List<SelectOption> getBidAgreementProductionAssociationContacts() {
    List<SelectOption> options = new List<SelectOption>();
    options.add(new SelectOption('', ''));
    for (Production_Associations__c productAssoc : [
      SELECT Id, Contact__c, Contact__r.Name
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :formBid.Production__c
        AND Contact__c != NULL
        AND RecordType.DeveloperName = 'Production_Contacts'
        AND Role__c INCLUDES (
          :('Primary ' + dashboard),
          :('CC: ' + dashboard),
          'Contract Signer'
        )
    ])
      options.add(
        new SelectOption(productAssoc.Contact__c, productAssoc.Contact__r.Name)
      );
    return options;
  }
  public void getAirInformationByBid() {
    airSegmentCities = '';
    for (Air__c airSegment : [
      SELECT
        Id,
        Air_Trip_Details__c,
        Departure_Date__c,
        Return_Date__c,
        Departure_City__c,
        Arrival_City__c,
        Departure_City__r.Airport_Code__c,
        Departure_City__r.Name,
        Departure_City__r.City__c,
        Departure_City__r.City__r.Name,
        Arrival_City__r.Airport_Code__c,
        Arrival_City__r.Name,
        Arrival_City__r.City__c,
        Arrival_City__r.City__r.Name
      FROM Air__c
      WHERE
        Air_Trip_Details__c = :formBid.Air__c
        AND RecordType.DeveloperName = 'Air_Segments'
    ]) {
      airSegmentCities = String.isNotBlank(airSegmentCities)
        ? airSegmentCities +
          ', ' +
          (airSegment.Departure_City__r.Airport_Code__c != null
            ? airSegment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (airSegment.Arrival_City__r.Airport_Code__c != null
            ? airSegment.Arrival_City__r.Airport_Code__c
            : '')
        : (airSegment.Departure_City__r.Airport_Code__c != null
            ? airSegment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (airSegment.Arrival_City__r.Airport_Code__c != null
            ? airSegment.Arrival_City__r.Airport_Code__c
            : '');
    }
  }
  public List<SelectOption> getBidAgreementCreditCards() {
    List<SelectOption> options = new List<SelectOption>();
    options.add(new SelectOption('', '-- Select --'));
    for (Credit_Card__c creditCard : [
      SELECT
        Id,
        Contact__r.FirstName,
        Contact__r.LastName,
        Credit_card_number__c,
        Expiration_Date__c
      FROM Credit_Card__c
      WHERE
        Contact__c IN (
          SELECT Contact__c
          FROM Production_Associations__c
          WHERE
            Production_Opp__c = :formBid.Production__c
            AND Contact__c != NULL
            AND RecordType.DeveloperName = 'Production_Contacts'
            AND Status__c = 'Associated'
        )
        AND Purpose__c INCLUDES (
          'All',
          'Ground Transportation Only',
          'Secondary'
        )
    ]) {
      options.add(
        new SelectOption(
          creditCard.Id,
          (String.isNotBlank(creditCard.Contact__r.FirstName)
            ? creditCard.Contact__r.FirstName + ' '
            : '') +
          creditCard.Contact__r.LastName +
          (creditCard.Credit_card_number__c != null
            ? ' ' + String.valueOf(creditCard.Credit_card_number__c)
            : '') +
          ', Exp:' +
          (String.isNotBlank(creditCard.Expiration_Date__c)
            ? creditCard.Expiration_Date__c
            : '')
        )
      );
    }
    return options;
  }
  public void changeBidAgreementContactPrimary() {
    List<Contact> bidAgreementContacts = [
      SELECT Id, FirstName, Name, Title, Phone, Email
      FROM Contact
      WHERE Id = :draft.Primary_Contact_Id__c
    ];
    bidAgreementPrimaryContact = !bidAgreementContacts.isEmpty()
      ? bidAgreementContacts[0]
      : new Contact();
    draft.Salutation__c =
      'Hi ' +
      (!bidAgreementContacts.isEmpty()
        ? bidAgreementContacts[0].FirstName
        : '') +
      ',';
  }
  public void changeBidAgreementProductionAssociationContact() {
    List<Contact> bidAgreementContacts = [
      SELECT Id, FirstName, Name, Title, Phone, Email
      FROM Contact
      WHERE Id = :draft.Production_Assoc_Contact_Id__c
    ];
    bidAgreementPrimaryContact = !bidAgreementContacts.isEmpty()
      ? bidAgreementContacts[0]
      : new Contact();
    draft.Salutation__c =
      'Hi ' +
      (!bidAgreementContacts.isEmpty()
        ? bidAgreementContacts[0].FirstName
        : '') +
      ',';
  }
  public void changeBidAgreementAttentionContact() {
    List<Contact> bidAgreementContacts = [
      SELECT Id, FirstName, Name, Title, Phone, Email
      FROM Contact
      WHERE Id = :draft.Attention__c
    ];
    bidAgreementAttentionContact = !bidAgreementContacts.isEmpty()
      ? bidAgreementContacts[0]
      : new Contact();
    draft.Salutation__c =
      'Hi ' +
      (!bidAgreementContacts.isEmpty()
        ? bidAgreementContacts[0].FirstName
        : '') +
      ',';
  }
  public void changeContactDataSelected() {
    String productionAssocContactId = (String.isNotBlank(
        draft.Production_Assoc_Contact_Id__c
      )
      ? draft.Production_Assoc_Contact_Id__c
      : '');
    List<SObject> results = String.isBlank(draft.Production_Assoc_Type__c) ||
      draft.Production_Assoc_Type__c == 'production_contacts'
      ? Database.query(
          'SELECT Id, FirstName, Name, Email FROM Contact WHERE Id =:productionAssocContactId'
        )
      : Database.query(
          'SELECT Id, FirstName, Name, Email FROM User WHERE Id =:productionAssocContactId'
        );
    if (!results.isEmpty())
      bidAgreementPrimaryContact = results[0];
    draft.Salutation__c =
      'Hi ' +
      (!results.isEmpty() ? bidAgreementPrimaryContact.get('Name') : '') +
      ',';
  }
  public void searchContactData() {
    dataContactPL = new List<SelectOption>();
    dataContactPL.add(new SelectOption('', '-- Select --'));
    bidAgreementPrimaryContact = new Contact();
    if (
      String.isBlank(draft.Production_Assoc_Type__c) ||
      draft.Production_Assoc_Type__c == 'production_contacts'
    ) {
      for (Production_Associations__c pa : [
        SELECT
          Id,
          Contact__c,
          Contact__r.Name,
          Contact__r.FirstName,
          Contact__r.LastName,
          Contact__r.Title,
          Contact__r.Email,
          Contact__r.Order__c
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :formBid.Production__c
          AND Contact__c != NULL
          AND Contact__r.Email != NULL
          AND Role__c INCLUDES (
            :('Primary ' + dashboard),
            :('CC: ' + dashboard),
            'Contract Signer'
          )
        ORDER BY Contact__r.Order__c ASC
      ]) {
        dataContactPL.add(
          new SelectOption(
            pa.Contact__c,
            (pa.Contact__r.Order__c != null
              ? pa.Contact__r.Order__c + ' - '
              : '') +
            pa.Contact__r.Name +
            ' - ' +
            pa.Contact__r.Email
          )
        );
        if (isNew) {
          draft.Production_Assoc_Type__c = 'production_contacts';
          if (
            String.isBlank(draft.Production_Assoc_Contact_Id__c) &&
            pa.Contact__r.Order__c == 1
          ) {
            draft.Production_Assoc_Contact_Id__c = pa.Contact__c;
            draft.Salutation__c = 'Hi ' + pa.Contact__r.FirstName + ',';
            bidAgreementPrimaryContact = pa.getSObject('Contact__r');
          } else {
            if (draft.Production_Assoc_Contact_Id__c == pa.Contact__c) {
              draft.Production_Assoc_Contact_Id__c = pa.Contact__c;
              draft.Salutation__c = 'Hi ' + pa.Contact__r.FirstName + ',';
              bidAgreementPrimaryContact = pa.getSObject('Contact__r');
            }
          }
        } else {
          if (draft.Production_Assoc_Contact_Id__c == pa.Contact__c)
            bidAgreementPrimaryContact = pa.getSObject('Contact__r');
        }
      }
    } else {
      for (Production_Associations__c pa : [
        SELECT Id, User__c, User__r.FirstName, User__r.Name, User__r.Email
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :formBid.Production__c
          AND RecordType.DeveloperName = 'Production_Coordinators'
          AND Team_Roles__c INCLUDES (
            :('Primary ' +
            dashboard +
            ' Coordinator'),
            :((dashboard == 'GT' ? 'Ground Travel' : dashboard) +
            ' back-end Coordinator')
          )
          AND User__c != NULL
        ORDER BY User__r.Name ASC
      ]) {
        dataContactPL.add(new SelectOption(pa.User__c, pa.User__r.Name));
        if (isNew && draft.Production_Assoc_Contact_Id__c == pa.User__c) {
          draft.Production_Assoc_Type__c = 'coordinators';
          draft.Production_Assoc_Contact_Id__c = pa.User__c;
          draft.Salutation__c = 'Hi ' + pa.User__r.FirstName + ',';
          bidAgreementPrimaryContact = pa.getSObject('User__r');
        } else if (draft.Production_Assoc_Contact_Id__c == pa.User__c)
          bidAgreementPrimaryContact = pa.getSObject('User__r');
      }
    }
  }
  public void saveBidAgreement() {
    try {
      update draft;
      draft = [
        SELECT
          Id,
          Name,
          Salutation__c,
          Attention__c,
          Primary_Contact_Id__c,
          Production_Assoc_Contact_Id__c,
          CC__c,
          Subject__C,
          Date__c,
          BCC__c,
          Body__c,
          Terms__c,
          CreatedBy.Name,
          CreatedDate,
          LastModifiedBy.Name,
          LastModifiedDate,
          Payment_Policy__c,
          Cancellation_Policy__c,
          Production_Assoc_Type__c,
          Credit_Card_Id__c
        FROM Draft__c
        WHERE Id = :draft.Id
      ];
      if (
        formValue == 'Form_Rate_Agreement__c' ||
        formValue == 'Form_Trip_Details_Update__c' ||
        formValue == 'Form_Transportation_Contract__c'
      ) {
        Bid__c bid = new Bid__c(id = formBid.id);
        bid.put(
          formValue == 'Form_Rate_Agreement__c'
            ? 'Rate_Agreement_Terms__c'
            : formValue == 'Form_Trip_Details_Update__c'
                ? 'Trip_Details_Update_Terms__c'
                : formValue == 'Form_Transportation_Contract__c'
                    ? 'Transportation_Contract_Terms__c'
                    : '',
          draft.Terms__c
        );
        bid.put(
          formValue == 'Form_Rate_Agreement__c'
            ? 'Rate_Agreement_Payment_Policy__c'
            : formValue == 'Form_Trip_Details_Update__c'
                ? 'Trip_Details_Update_Payment_Policy__c'
                : formValue == 'Form_Transportation_Contract__c'
                    ? 'Transportation_Contract_Payment_Policy__c'
                    : '',
          draft.Payment_Policy__c
        );
        bid.put(
          formValue == 'Form_Rate_Agreement__c'
            ? 'Rate_Agreement_Cancellation_Policy__c'
            : formValue == 'Form_Trip_Details_Update__c'
                ? 'Trip_Details_Update_Cancel_Policy__c'
                : formValue == 'Form_Transportation_Contract__c'
                    ? 'Transportation_Contract_Cancel_Policy__c'
                    : '',
          draft.Cancellation_Policy__c
        );
        update bid;
      }
      if (String.isNotBlank(selectedGcqId))
        generateGCQ();
      String emailBody =
        (String.isNotBlank(draft.Salutation__c)
          ? draft.Salutation__c + '<br/><br/>'
          : '') +
        (String.isNotBlank(draft.Body__c)
          ? draft.Body__c.removeStartIgnoreCase('<p>')
              .removeEndIgnoreCase('</p>')
          : '') +
        (String.isNotBlank(primaryCoordinatorName)
          ? '<br/>' + primaryCoordinatorName
          : '') +
        '<br/>' +
        dashboard +
        ' Coordinator';
      if (isCongaSignSent) {
        emailResult = send(
          form_to,
          form_cc,
          form_bcc,
          draft.Subject__c,
          emailBody,
          null,
          bidAgreement_congaEmailFromId
        );
        isCongaSignSent = false;
      } else if (String.isNotBlank(bidAgreement_congaEmailTemplateId))
        update new APXTConga4__Conga_Email_Template__c(
          id = bidAgreement_congaEmailTemplateId,
          APXTConga4__HTMLBody__c = emailBody
        );
    } catch (Exception e) {
      System.debug(
        'Dashboard_Tab_Contract_Forms.saveBidAgreement() - Exception: ' +
        e.getMessage()
      );
    }
    if (bidParentSObject == 'Air')
      openPreviewFinalTicketedConfirmation();
  }
  public void deactivateBidAgreement() {
    try {
      delete draft;
      Bid__c bid = new Bid__c(id = formBid.id);
      bid.put(formValue, null);
      bid.put(
        formValue == 'Form_Rate_Agreement__c'
          ? 'Rate_Agreement_Last_Send_Date__c'
          : formValue == 'Form_Trip_Details_Update__c'
              ? 'Trip_Details_Update_Last_Send_Date__c'
              : formValue == 'Form_Transportation_Contract__c'
                  ? 'Transportation_Contract_Last_Send_Date__c'
                  : formValue == 'Form_Contract_to_Client__c'
                      ? 'Contract_to_Client_Last_Send_Date__c'
                      : formValue == 'Form_Counter_Needed__c'
                          ? 'Counter_Needed_Last_Send_Date__c'
                          : formValue == 'Form_Final_Contract__c'
                              ? 'Final_Contract_Last_Send_Date__c'
                              : formValue == 'Form_Email_Confirmation__c'
                                  ? 'Email_Confirmation_Last_Send_Date__c'
                                  : formValue == 'Form_Credit_Card_Change__c'
                                      ? 'Credit_Card_Last_Send_Date__c'
                                      : formValue ==
                                          'Form_Cancellation_Letter__c'
                                          ? 'Cancellation_Last_Send_Date__c'
                                          : formValue == 'Form_Deposit_Due__c'
                                              ? 'Deposit_Due_Last_Send_Date__c'
                                              : formValue ==
                                                  'Form_Utilization__c'
                                                  ? 'Utilization_Last_Send_Date__c'
                                                  : formValue ==
                                                      'Form_Names_Final_Payment__c'
                                                      ? 'Names_Final_Payment_Last_Send_Date__c'
                                                      : formValue ==
                                                          'Form_Final_Choice__c'
                                                          ? 'Final_Choice_Last_Send_Date__c'
                                                          : formValue ==
                                                              'Form_Ticketed_Confirmation__c'
                                                              ? 'Ticketed_Confirmation_Last_Send_Date__c'
                                                              /*: formValue ==                                  //Changes Added as per 175349270
                                                              'Form_Create_GCIP__c '
                                                              ? 'Form_Create_GCIP_Last_Send_Date__c'
                                                              */
                                                              : formValue ==
                                                                  'Form_Final_Air_Confirmation__c'
                                                                  ? 'Final_Air_Confirmation_Last_Send_Date__c'
                                                                  : '',
        null
      );
      bid.put(
        formValue == 'Form_Rate_Agreement__c'
          ? 'Rate_Agreement_Last_Send_By__c'
          : formValue == 'Form_Trip_Details_Update__c'
              ? 'Trip_Details_Update_Last_Send_By__c'
              : formValue == 'Form_Transportation_Contract__c'
                  ? 'Transportation_Contract_Last_Send_By__c'
                  : formValue == 'Form_Contract_to_Client__c'
                      ? 'Contract_to_Client_Last_Send_By__c'
                      : formValue == 'Form_Counter_Needed__c'
                          ? 'Counter_Needed_Last_Send_By__c'
                          : formValue == 'Form_Final_Contract__c'
                              ? 'Final_Contract_Last_Send_By__c'
                              : formValue == 'Form_Email_Confirmation__c'
                                  ? 'Email_Confirmation_Last_Send_By__c'
                                  : formValue == 'Form_Credit_Card_Change__c'
                                      ? 'Credit_Card_Last_Send_By__c'
                                      : formValue ==
                                          'Form_Cancellation_Letter__c'
                                          ? 'Cancellation_Last_Send_By__c'
                                          : formValue == 'Form_Deposit_Due__c'
                                              ? 'Deposit_Due_Last_Send_By__c'
                                              : formValue ==
                                                  'Form_Utilization__c'
                                                  ? 'Utilization_Last_Send_By__c'
                                                  : formValue ==
                                                      'Form_Names_Final_Payment__c'
                                                      ? 'Names_Final_Payment_Last_Send_By__c'
                                                      : formValue ==
                                                          'Form_Final_Choice__c'
                                                          ? 'Final_Choice_Last_Send_By__c'
                                                          : formValue ==
                                                              'Form_Ticketed_Confirmation__c'
                                                              ? 'Ticketed_Confirmation_Last_Send_By__c'
                                                              : formValue ==
                                                                  'Form_Final_Air_Confirmation__c'
                                                                  ? 'Final_Air_Confirmation_Last_Send_By__c'
                                                                  : '',
        null
      );
      update bid;
      for (Dashboard_Tab_Contract_Forms.FormWrapper formButton : formList1)
        if (formButton.value.equals(formValue))
          formButton.draftCode = null;
      for (Dashboard_Tab_Contract_Forms.FormWrapper formButton : formList2)
        if (formButton.value.equals(formValue))
          formButton.draftCode = null;
    } catch (Exception e) {
      System.debug(
        'Dashboard_Tab_Contract_Forms.deactivateBidAgreement() - Exception: ' +
        e.getMessage()
      );
    }
  }
  @RemoteAction
  public static String searchContactEmail(String query) {
    query = '%' + query + '%';
    List<wrapperData> Contacts = new List<wrapperData>();
    for (Contact contact : [
      SELECT Id, Name, Email
      FROM Contact
      WHERE (Name LIKE :query OR Email LIKE :query) AND email != NULL
      LIMIT 20
    ])
      Contacts.add(
        new wrapperData(
          contact.Id,
          contact.Name +
          ', ' +
          contact.Email,
          contact.Email
        )
      );
    return JSON.serialize(Contacts);
  }
  //End BidAgreement Methods
  ///Attach GCQ Methods
  public void openAttachGcq() {
    attachGcq_departureDate = attachGcq_arrivalDate = null;
    gcqSubtripsMap = new Map<SObject, List<SObject>>();
    bidSubtripsMap = new Map<Id, SObject>();
    searchGcqsMap = new Map<Id, GcqWrapper>();
    isAttachGCQRendered = isGcqEmpty = true;
    isGcqSearched = false;
  }
  public void searchAttachGcq() {
    if (
      String.isNotBlank(attachGcq_departureDate) &&
      String.isNotBlank(attachGcq_arrivalDate)
    ) {
      gcqSubtripsMap.clear();
      bidSubtripsMap.clear();
      searchGcqsMap.clear();
      if (bidParentSObject == 'Ground') {
        for (Sub_Trip_GCQ__c subtripGcq : [
          SELECT
            GCQ_Details__r.Name,
            GT_Sub_Trip_Details__r.id,
            GT_Sub_Trip_Details__r.Description__c,
            GT_Sub_Trip_Details__r.Bid_Sub_Trip__c,
            GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__c,
            GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.Name,
            GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.Description__c
          FROM Sub_Trip_GCQ__c
          WHERE
            ((GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.Start_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.Start_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            ))
            OR (GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.End_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND GT_Sub_Trip_Details__r.Bid_Sub_Trip__r.GT__r.End_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            )))
            AND GT_Sub_Trip_Details__r.Production_Ground__c = :formBid.Production__c
          ORDER BY GCQ_Details__r.Name, GT_Sub_Trip_Details__r.Trip_Order__c
        ]) {
          if (gcqSubtripsMap.get(subtripGcq.GCQ_Details__r) == null)
            gcqSubtripsMap.put(
              subtripGcq.GCQ_Details__r,
              new List<SObject>{ subtripGcq.GT_Sub_Trip_Details__r }
            );
          else
            gcqSubtripsMap.get(subtripGcq.GCQ_Details__r)
              .add(subtripGcq.GT_Sub_Trip_Details__r);
          bidSubtripsMap.put(
            subtripGcq.GT_Sub_Trip_Details__r.id,
            subtripGcq.GT_Sub_Trip_Details__r
          );
        }
        for (Ground__c bidSubtrip : [
          SELECT
            id,
            (
              SELECT
                id,
                Start_Date__c,
                Start_Date_Time__c,
                End_Date__c,
                End_Date_Time__c
              FROM GTTravels__r
              ORDER BY Line__c
              LIMIT 1
            )
          FROM Ground__c
          WHERE id IN :bidSubtripsMap.keySet()
          ORDER BY Trip_Order__c
        ])
          bidSubtripsMap.put(bidSubtrip.id, bidSubtrip);
        isGcqEmpty = bidSubtripsMap.values().isEmpty();
      } else if (bidParentSObject == 'Freight') {
        for (Sub_Trip_FCQ__c subtripFcq : [
          SELECT
            FCQ_Details__r.Name,
            Freight_Sub_Trip_Details__r.id,
            Freight_Sub_Trip_Details__r.Description__c,
            Freight_Sub_Trip_Details__r.Bid_Sub_Trip__c,
            Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__c,
            Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Name,
            Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Description__c
          FROM Sub_Trip_FCQ__c
          WHERE
            ((Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Start_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Start_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            ))
            OR (Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.End_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.End_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            )))
            AND Freight_Sub_Trip_Details__r.Production__c = :formBid.Production__c
          ORDER BY
            FCQ_Details__r.Name,
            Freight_Sub_Trip_Details__r.Trip_Order__c
        ]) {
          if (gcqSubtripsMap.get(subtripFcq.FCQ_Details__r) == null)
            gcqSubtripsMap.put(
              subtripFcq.FCQ_Details__r,
              new List<SObject>{ subtripFcq.Freight_Sub_Trip_Details__r }
            );
          else
            gcqSubtripsMap.get(subtripFcq.FCQ_Details__r)
              .add(subtripFcq.Freight_Sub_Trip_Details__r);
          bidSubtripsMap.put(
            subtripFcq.Freight_Sub_Trip_Details__r.id,
            subtripFcq.Freight_Sub_Trip_Details__r
          );
        }
        for (Freight__c bidSubtrip : [
          SELECT
            id,
            (
              SELECT
                id,
                Start_Date__c,
                Start_Date_Time__c,
                End_Date__c,
                End_Date_Time__c
              FROM FreightEquipments__r
              ORDER BY Line__c
              LIMIT 1
            )
          FROM Freight__c
          WHERE id IN :bidSubtripsMap.keySet()
          ORDER BY Trip_Order__c
        ])
          bidSubtripsMap.put(bidSubtrip.id, bidSubtrip);
        isGcqEmpty = bidSubtripsMap.values().isEmpty();
      } else if (bidParentSObject == 'Air') {
        for (Segment_GCQ__c SegmentGCQ : [
          SELECT id, GCQ_Details__c
          FROM Segment_GCQ__c
          WHERE
            ((Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Departure_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Departure_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            ))
            OR (Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Return_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Return_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            ))
            OR (Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Departure_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Departure_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            ))
            OR (Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Return_Date__c >= :Date.valueOf(
              attachGcq_departureDate
            )
            AND Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Return_Date__c <= :Date.valueOf(
              attachGcq_arrivalDate
            )))
            AND Air_Segments__r.Production__c = :formBid.Production__c
        ])
          searchGcqsMap.put(SegmentGCQ.GCQ_Details__c, null);
        for (Air__c gcq : [
          SELECT
            id,
            Name,
            (
              SELECT
                id,
                Air_Segments__r.Air_Itinerary_Details__c,
                Air_Segments__r.Air_Itinerary_Details__r.Description__c,
                Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__c,
                Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__c,
                Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Name,
                Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Description__c,
                Air_Segments__r.Air_Deviation_Details__c,
                Air_Segments__r.Air_Deviation_Details__r.Deviation_Order_Formula_Conga__c,
                Air_Segments__r.Air_Deviation_Details__r.Description__c,
                Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__c,
                Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__c,
                Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Name,
                Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Description__c,
                Air_Segments__r.Order__c,
                Air_Segments__r.Departure_Date__c
              FROM Segments__r
              ORDER BY
                Air_Segments__r.Air_Deviation_Details__r.Deviation_Order_Conga__c,
                Air_Segments__r.Order__c
            )
          FROM Air__c
          WHERE id IN :searchGcqsMap.keySet()
        ]) {
          searchGcqsMap.put(gcq.id, new GcqWrapper(gcq.Name));
          for (Segment_GCQ__c segmentGCQ : gcq.Segments__r) {
            if (
              String.isNotEmpty(
                segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c
              )
            ) {
              if (
                !searchGcqsMap.get(gcq.id)
                  .itinerarySegmentsMap.containsKey(
                    segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r
                  )
              )
                searchGcqsMap.get(gcq.id)
                  .itinerarySegmentsMap.put(
                    segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r,
                    new List<Air__c>()
                  );
              searchGcqsMap.get(gcq.id)
                .itinerarySegmentsMap.get(
                  segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r
                )
                .add(segmentGCQ.Air_Segments__r);
              searchGcqsMap.get(gcq.id)
                .tripId = segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Name;
              searchGcqsMap.get(gcq.id)
                .tripDescription = segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Air__r.Description__c;
              searchGcqsMap.get(gcq.id)
                .bidId = segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__c;
            } else {
              if (
                !searchGcqsMap.get(gcq.id)
                  .deviationSegmentsMap.containsKey(
                    segmentGCQ.Air_Segments__r.Air_Deviation_Details__r
                  )
              )
                searchGcqsMap.get(gcq.id)
                  .deviationSegmentsMap.put(
                    segmentGCQ.Air_Segments__r.Air_Deviation_Details__r,
                    new List<Air__c>()
                  );
              searchGcqsMap.get(gcq.id)
                .deviationSegmentsMap.get(
                  segmentGCQ.Air_Segments__r.Air_Deviation_Details__r
                )
                .add(segmentGCQ.Air_Segments__r);
              searchGcqsMap.get(gcq.id)
                .tripId = segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Name;
              searchGcqsMap.get(gcq.id)
                .tripDescription = segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Air__r.Description__c;
              searchGcqsMap.get(gcq.id)
                .bidId = segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__c;
            }
          }
        }
        isGcqEmpty = searchGcqsMap.isEmpty();
      }
      isGcqSearched = true;
    }
  }
  public void generateGCQ() {
    Map<Id, Air__c> itinerariesMap = new Map<Id, Air__c>();
    Map<Id, Air__c> deviationsMap = new Map<Id, Air__c>();
    Map<Id, String> rateDetailsMap = new Map<Id, String>();
    Air__c congaAirGcq = new Air__c(
      id = selectedGcqId,
      GCQ_Main_Travel_Information_Conga__c = '',
      GCQ_Deviation_Travel_Information_Conga__c = ''
    );
    for (Segment_GCQ__c segmentGCQ : [
      SELECT
        Air_Segments__r.Air_Itinerary_Details__c,
        Air_Segments__r.Air_Itinerary_Details__r.Trip_Type__c,
        Air_Segments__r.Air_Itinerary_Details__r.Group_Type__c,
        Air_Segments__r.Air_Itinerary_Details__r.Description__c,
        Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name,
        Air_Segments__r.Air_Deviation_Details__c,
        Air_Segments__r.Air_Deviation_Details__r.Deviation_Order_Conga__c,
        Air_Segments__r.Air_Deviation_Details__r.Trip_Type__c,
        Air_Segments__r.Air_Deviation_Details__r.Group_Type__c,
        Air_Segments__r.Air_Deviation_Details__r.Description__c,
        Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name,
        Air_Segments__r.Order__c,
        Air_Segments__r.Departure_Date__c,
        Air_Segments__r.Dep_Time__c,
        Air_Segments__r.Departure_City__c,
        Air_Segments__r.Departure_City__r.Name,
        Air_Segments__r.Departure_City__r.Airport_Code__c,
        Air_Segments__r.Arrival_Date__c,
        Air_Segments__r.Arr_Time__c,
        Air_Segments__r.Arrival_City__c,
        Air_Segments__r.Arrival_City__r.Name,
        Air_Segments__r.Arrival_City__r.Airport_Code__c,
        Air_Segments__r.Flight_No__c,
        Air_Segments__r.Flight_Duration_hrs__c,
        Air_Segments__r.Flight_Duration_Mins__c,
        Air_Segments__r.Class__c,
        Air_Segments__r.Equip_Type__c,
        Air_Segments__r.Number_of_Seats__c,
        Air_Segments__r.Operated_by__c
      FROM Segment_GCQ__c
      WHERE GCQ_Details__c = :selectedGcqId
      ORDER BY
        Air_Segments__r.Air_Deviation_Details__r.Deviation_Order_Conga__c,
        Air_Segments__r.Order__c
    ]) {
      if (
        String.isNotEmpty(segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c)
      ) {
        if (
          !itinerariesMap.containsKey(
            segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c
          )
        )
          itinerariesMap.put(
            segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c,
            new Air__c(
              id = segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c,
              GCQ_Main_Travel_Information_Conga__c = ''
            )
          );
        itinerariesMap.get(segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c)
            .GCQ_Main_Travel_Information_Conga__c +=
          (String.isNotBlank(
              itinerariesMap.get(
                  segmentGCQ.Air_Segments__r.Air_Itinerary_Details__c
                )
                .GCQ_Main_Travel_Information_Conga__c
            )
            ? '<tr><td width="726" height="15"></td></tr>'
            : '') +
          '<tr><td width="726"><table width="740" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .capitalize()
            : '') +
          '</strong>' +
          '</td></tr>' +
          (String.isNotEmpty(segmentGCQ.Air_Segments__r.Operated_by__c)
            ? '<tr><td width="726" height="20" align="left" style="padding:3px 4px;">' +
              'Operated by ' +
              String.valueOf(segmentGCQ.Air_Segments__r.Operated_by__c) +
              '</td></tr>'
            : '') +
          '</table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="65" height="20" align="left" style="padding:3px 4px;font-size:12px;">AIRLINE</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotEmpty(
              segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name
            )
            ? segmentGCQ.Air_Segments__r.Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="100" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Flight_No__c)
            ? segmentGCQ.Air_Segments__r.Flight_No__c
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">CLASS</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Class__c)
            ? segmentGCQ.Air_Segments__r.Class__c
            : '') +
          '</td></tr><tr><th width="65" height="20" align="left" style="padding:3px 4px;">DEPART</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_City__c != null
            ? segmentGCQ.Air_Segments__r.Departure_City__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">TIME</th><td width="100" height="20" align="left" style="padding:3px 0 3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Dep_Time__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  segmentGCQ.Air_Segments__r.Dep_Time__c
                )
                .format('h:mm a')
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">EQP</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Equip_Type__c)
            ? segmentGCQ.Air_Segments__r.Equip_Type__c
            : '') +
          '</td></tr><tr><th width="65" height="20" align="left" style="padding:3px 4px;">ARRIVE</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Arrival_City__c != null
            ? segmentGCQ.Air_Segments__r.Arrival_City__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">TIME</th><td width="100" height="20" align="left" style="padding:3px 0 3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Arr_Time__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  segmentGCQ.Air_Segments__r.Arr_Time__c
                )
                .format('h:mm a')
            : '') +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Arrival_Date__c != null &&
            !segmentGCQ.Air_Segments__r.Departure_Date__c.isSameDay(
              segmentGCQ.Air_Segments__r.Arrival_Date__c
            )
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">DURATION</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Flight_Duration_hrs__c != null
            ? String.valueOf(
                segmentGCQ.Air_Segments__r.Flight_Duration_hrs__c
              ) + 'HRS '
            : '') +
          (segmentGCQ.Air_Segments__r.Flight_Duration_Mins__c != null
            ? String.valueOf(
                segmentGCQ.Air_Segments__r.Flight_Duration_Mins__c
              ) + 'MINS'
            : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      } else {
        if (
          !deviationsMap.containsKey(
            segmentGCQ.Air_Segments__r.Air_Deviation_Details__c
          )
        )
          deviationsMap.put(
            segmentGCQ.Air_Segments__r.Air_Deviation_Details__c,
            new Air__c(
              id = segmentGCQ.Air_Segments__r.Air_Deviation_Details__c,
              GCQ_Deviation_Travel_Information_Conga__c = '',
              Deviation_Order_Conga__c = segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Deviation_Order_Conga__c
            )
          );
        deviationsMap.get(segmentGCQ.Air_Segments__r.Air_Deviation_Details__c)
            .GCQ_Deviation_Travel_Information_Conga__c +=
          (String.isNotBlank(
              deviationsMap.get(
                  segmentGCQ.Air_Segments__r.Air_Deviation_Details__c
                )
                .GCQ_Deviation_Travel_Information_Conga__c
            )
            ? '<tr><td width="726" height="15"></td></tr>'
            : '') +
          '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .capitalize()
            : '') +
          '</strong>' +
          '</td></tr>' +
          (String.isNotEmpty(segmentGCQ.Air_Segments__r.Operated_by__c)
            ? '<tr><td width="726" height="20" align="left" style="padding:3px 4px;">' +
              'Operated by ' +
              String.valueOf(segmentGCQ.Air_Segments__r.Operated_by__c) +
              '</td></tr>'
            : '') +
          '</table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="65" height="20" align="left" style="padding:3px 4px;font-size:12px;">AIRLINE</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotEmpty(
              segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name
            )
            ? segmentGCQ.Air_Segments__r.Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="100" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Flight_No__c)
            ? segmentGCQ.Air_Segments__r.Flight_No__c
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">CLASS</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Class__c)
            ? segmentGCQ.Air_Segments__r.Class__c
            : '') +
          '</td></tr><tr><th width="65" height="20" align="left" style="padding:3px 4px;">DEPART</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_City__c != null
            ? segmentGCQ.Air_Segments__r.Departure_City__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">TIME</th><td width="100" height="20" align="left" style="padding:3px 0 3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Dep_Time__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  segmentGCQ.Air_Segments__r.Dep_Time__c
                )
                .format('h:mm a')
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">EQP</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(segmentGCQ.Air_Segments__r.Equip_Type__c)
            ? segmentGCQ.Air_Segments__r.Equip_Type__c
            : '') +
          '</td></tr><tr><th width="65" height="20" align="left" style="padding:3px 4px;">ARRIVE</th><td width="230" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Arrival_City__c != null
            ? segmentGCQ.Air_Segments__r.Arrival_City__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">TIME</th><td width="100" height="20" align="left" style="padding:3px 0 3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Arr_Time__c != null
            ? Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Departure_Date__c,
                  segmentGCQ.Air_Segments__r.Arr_Time__c
                )
                .format('h:mm a')
            : '') +
          (segmentGCQ.Air_Segments__r.Departure_Date__c != null &&
            segmentGCQ.Air_Segments__r.Arrival_Date__c != null &&
            !segmentGCQ.Air_Segments__r.Departure_Date__c.isSameDay(
              segmentGCQ.Air_Segments__r.Arrival_Date__c
            )
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  segmentGCQ.Air_Segments__r.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="65" height="20" align="left" style="padding:3px 4px;">DURATION</th><td width="131" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (segmentGCQ.Air_Segments__r.Flight_Duration_hrs__c != null
            ? String.valueOf(
                segmentGCQ.Air_Segments__r.Flight_Duration_hrs__c
              ) + 'HRS '
            : '') +
          (segmentGCQ.Air_Segments__r.Flight_Duration_Mins__c != null
            ? String.valueOf(
                segmentGCQ.Air_Segments__r.Flight_Duration_Mins__c
              ) + 'MINS'
            : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      }
    }
    for (Revenue__c rate : [
      SELECT
        id,
        Rate_currency__c,
        Service_Fees__c,
        Additional_Fees__c,
        Total_Taxes__c,
        Total_Price__c,
        of_seats__c,
        Record_Locator__c,
        Deviation__c
      FROM Revenue__c
      WHERE
        Bid__c = :formBid.id
        AND RecordType.DeveloperName = 'Air_Rate_Commission'
    ]) {
      if (!rateDetailsMap.containsKey(rate.Deviation__c))
        rateDetailsMap.put(rate.Deviation__c, '');
      rateDetailsMap.put(
        rate.Deviation__c,
        rateDetailsMap.get(rate.Deviation__c) +
        '<tr><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Rate_currency__c != null
          ? '$ ' + String.valueOf(rate.Rate_currency__c)
          : '') +
        '</td><td width="106" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Taxes__c != null
          ? '$ ' + String.valueOf(rate.Total_Taxes__c)
          : '') +
        '</td><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Service_Fees__c != null
          ? '$ ' + String.valueOf(rate.Service_Fees__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Price__c != null
          ? '$ ' + String.valueOf(rate.Total_Price__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (String.isNotBlank(rate.Record_Locator__c)
          ? rate.Record_Locator__c
          : '') +
        '</td><td width="120" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.of_seats__c != null ? String.valueOf(rate.of_seats__c) : '') +
        '</td></tr>'
      );
    }
    for (Air__c itinerary : itinerariesMap.values())
      congaAirGcq.GCQ_Main_Travel_Information_Conga__c +=
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top">' +
        (rateDetailsMap.containsKey(null)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(null) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(null)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        itinerary.GCQ_Main_Travel_Information_Conga__c +
        '</table>';
    for (Air__c deviation : deviationsMap.values())
      congaAirGcq.GCQ_Deviation_Travel_Information_Conga__c +=
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><tr><td width="726" height="20"></td></tr><tr><th width="726" align="left" style="margin-top:10px;font-size:18px;">DEVIATION ' +
        (deviation.Deviation_Order_Conga__c != null
          ? String.valueOf(deviation.Deviation_Order_Conga__c)
          : '') +
        '</th></tr><tr><td width="726" height="10"></td></tr>' +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(deviation.id) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        deviation.GCQ_Deviation_Travel_Information_Conga__c +
        '</table>';
    try {
      update congaAirGcq;
    } catch (DmlException e) {
      System.debug(
        'Dashboard_Tab_Contract_Forms.generateGCQ() - DmlException: ' +
        e.getMessage()
      );
    }
  }
  //End Attach GCQ Methods
  ///FinalChoice Methods
  public void openPreviewFinalTicketedConfirmation() {
    Map<Id, Air__c> itinerariesMap = new Map<Id, Air__c>();
    Map<Id, Air__c> deviationsMap = new Map<Id, Air__c>();
    Map<Id, String> rateDetailsMap = new Map<Id, String>();
    for (Air__c air : [
      SELECT
        id,
        Air_Itinerary_Details__c,
        Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name,
        Air_Deviation_Details__c,
        Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name,
        Order__c,
        Departure_Date__c,
        Dep_Time__c,
        Departure_City__c,
        Departure_City__r.Name,
        Arrival_Date__c,
        Arr_Time__c,
        Arrival_City__c,
        Arrival_City__r.Name,
        Flight_No__c,
        Flight_Duration_hrs__c,
        Flight_Duration_Mins__c,
        Class__c,
        Equip_Type__c,
        Number_of_Seats__c,
        Operated_by__c
      FROM Air__c
      WHERE
        (Air_Itinerary_Details__r.Bid_Itinerary__c = :formBid.id
        OR Air_Deviation_Details__r.Bid_Deviation__c = :formBid.id)
        AND RecordType.DeveloperName = 'Air_Segments'
      ORDER BY Departure_Date__c
    ]) {
      if (String.isNotEmpty(air.Air_Itinerary_Details__c)) {
        if (!itinerariesMap.containsKey(air.Air_Itinerary_Details__c))
          itinerariesMap.put(
            air.Air_Itinerary_Details__c,
            new Air__c(
              id = air.Air_Itinerary_Details__c,
              Travel_Date_Conga__c = air.Departure_Date__c,
              Final_Travel_Information_Conga__c = ''
            )
          );
        itinerariesMap.get(air.Air_Itinerary_Details__c)
            .Final_Travel_Information_Conga__c +=
          (String.isNotBlank(
              itinerariesMap.get(air.Air_Itinerary_Details__c)
                .Final_Travel_Information_Conga__c
            )
            ? '<tr><td width="726" height="20"></td></tr>'
            : '') +
          '<tr><td width="726"><table width="740" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (air.Departure_Date__c != null
            ? Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          '</strong>' +
          (air.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .toUpperCase()
            : '') +
          '</td></tr>' +
          (String.isNotEmpty(air.Operated_by__c)
            ? '<tr><td width="726" height="20" align="left" style="padding:3px 4px;">' +
              'Operated by ' +
              String.valueOf(air.Operated_by__c) +
              '</td></tr>'
            : '') +
          '</table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="70" height="20" align="left" style="padding:3px 4px;font-size:12px;">AIRLINE</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_City__c != null ? air.Departure_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Flight_No__c) ? air.Flight_No__c : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">TO</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Arrival_City__c != null ? air.Arrival_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">DEPARTS</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Dep_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Dep_Time__c)
                .format('h:mm a')
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">FROM</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotEmpty(
              air.Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name
            )
            ? air.Air_Itinerary_Details__r.Bid_Itinerary__r.Vendor__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">ARRIVES</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Arr_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Arr_Time__c)
                .format('h:mm a')
            : '') +
          (air.Departure_Date__c != null &&
            air.Arrival_Date__c != null &&
            !air.Departure_Date__c.isSameDay(air.Arrival_Date__c)
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  air.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">DUR</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Flight_Duration_hrs__c != null
            ? String.valueOf(air.Flight_Duration_hrs__c) + 'HRS '
            : '') +
          (air.Flight_Duration_Mins__c != null
            ? String.valueOf(air.Flight_Duration_Mins__c) + 'MINS'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">AIRCRAFT</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Equip_Type__c) ? air.Equip_Type__c : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      } else {
        if (!deviationsMap.containsKey(air.Air_Deviation_Details__c))
          deviationsMap.put(
            air.Air_Deviation_Details__c,
            new Air__c(
              id = air.Air_Deviation_Details__c,
              Final_Travel_Information_Conga__c = ''
            )
          );
        deviationsMap.get(air.Air_Deviation_Details__c)
            .Final_Travel_Information_Conga__c +=
          (String.isNotBlank(
              deviationsMap.get(air.Air_Deviation_Details__c)
                .Final_Travel_Information_Conga__c
            )
            ? '<tr><td width="726" height="20"></td></tr>'
            : '') +
          '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (air.Departure_Date__c != null
            ? Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          '</strong>' +
          (air.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .toUpperCase()
            : '') +
          '</td></tr>' +
          (String.isNotEmpty(air.Operated_by__c)
            ? '<tr><td width="726" height="20" align="left" style="padding:3px 4px;">' +
              'Operated by ' +
              String.valueOf(air.Operated_by__c) +
              '</td></tr>'
            : '') +
          '</table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="70" height="20" align="left" style="padding:3px 4px;font-size:12px;">AIRLINE</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_City__c != null ? air.Departure_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Flight_No__c) ? air.Flight_No__c : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">TO</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Arrival_City__c != null ? air.Arrival_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">DEPARTS</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Dep_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Dep_Time__c)
                .format('h:mm a')
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">FROM</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotEmpty(
              air.Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name
            )
            ? air.Air_Deviation_Details__r.Bid_Deviation__r.Vendor__r.Name
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">ARRIVES</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Arr_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Arr_Time__c)
                .format('h:mm a')
            : '') +
          (air.Departure_Date__c != null &&
            air.Arrival_Date__c != null &&
            !air.Departure_Date__c.isSameDay(air.Arrival_Date__c)
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  air.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">DUR</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Flight_Duration_hrs__c != null
            ? String.valueOf(air.Flight_Duration_hrs__c) + 'HRS '
            : '') +
          (air.Flight_Duration_Mins__c != null
            ? String.valueOf(air.Flight_Duration_Mins__c) + 'MINS'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">AIRCRAFT</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Equip_Type__c) ? air.Equip_Type__c : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      }
    }
    for (Revenue__c rate : [
      SELECT
        id,
        Rate_currency__c,
        Service_Fees__c,
        Additional_Fees__c,
        Total_Taxes__c,
        Total_Price__c,
        of_seats__c,
        Record_Locator__c,
        Deviation__c
      FROM Revenue__c
      WHERE
        Bid__c = :formBid.id
        AND RecordType.DeveloperName = 'Air_Rate_Commission'
    ]) {
      if (!rateDetailsMap.containsKey(rate.Deviation__c))
        rateDetailsMap.put(rate.Deviation__c, '');
      rateDetailsMap.put(
        rate.Deviation__c,
        rateDetailsMap.get(rate.Deviation__c) +
        '<tr><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Rate_currency__c != null
          ? '$ ' + String.valueOf(rate.Rate_currency__c)
          : '') +
        '</td><td width="106" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Taxes__c != null
          ? '$ ' + String.valueOf(rate.Total_Taxes__c)
          : '') +
        '</td><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Service_Fees__c != null
          ? '$ ' + String.valueOf(rate.Service_Fees__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Price__c != null
          ? '$ ' + String.valueOf(rate.Total_Price__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (String.isNotBlank(rate.Record_Locator__c)
          ? rate.Record_Locator__c
          : '') +
        '</td><td width="120" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.of_seats__c != null ? String.valueOf(rate.of_seats__c) : '') +
        '</td></tr>'
      );
    }
    for (Air__c itinerary : itinerariesMap.values())
      itinerary.Final_Travel_Information_Conga__c =
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top">' +
        (rateDetailsMap.containsKey(null)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(null) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(null)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        itinerary.Final_Travel_Information_Conga__c +
        '</table>';
    for (Air__c deviation : deviationsMap.values())
      deviation.Final_Travel_Information_Conga__c =
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top">' +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(deviation.id) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        deviation.Final_Travel_Information_Conga__c +
        '</table>';
    try {
      if (!itinerariesMap.values().isEmpty())
        update itinerariesMap.values();
      if (!deviationsMap.values().isEmpty())
        update deviationsMap.values();
    } catch (DmlException e) {
      System.debug(
        'Dashboard_Tab_Contract_Forms.openPreviewFinalTicketedConfirmation() - DmlException: ' +
        e.getMessage()
      );
    }
  }
  //End FinalChoice Methods
  //Attachs
  public void openAttachDocs() {
    attachDocumentList = new List<ContentDocument>();
    if (attachdocument_objectid != null && attachdocument_objectid != '') {
      Set<String> contentDocumentIds = new Set<String>();
      for (ContentDocumentLink cdl : [
        SELECT Id, LinkedEntityId, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :attachdocument_objectid
      ])
        contentDocumentIds.add(cdl.ContentDocumentId);
      attachDocumentList = [
        SELECT Id, Title, FileExtension, CreatedDate
        FROM ContentDocument
        WHERE Id IN :contentDocumentIds
      ];
    }
    isAttachsRendered = true;
  }
  public void doAttachmentLast() {
    if (filename != null && body != null) {
      try {
        ContentVersion conVer = new ContentVersion();
        conVer.PathOnClient = '/' + filename;
        conVer.Title = filename.split('\.')[0];
        conVer.VersionData = (body.length() > 100
          ? EncodingUtil.base64Decode(
              body.subString(0, 100).split(',')[1] +
              body.substring(100, body.length())
            )
          : EncodingUtil.base64Decode(body.split(',')[1]));
        insert conVer;

        ContentVersion contentver = [
          SELECT ContentDocumentId, ContentDocument.FileExtension
          FROM ContentVersion
          WHERE Id = :conVer.Id
        ];

        //Create ContentDocumentLink
        ContentDocumentLink cDe = new ContentDocumentLink();
        cDe.ContentDocumentId = contentver.ContentDocumentId;
        cDe.LinkedEntityId = documentRelationId;
        cDe.ShareType = 'V';
        cDe.Visibility = 'AllUsers';
        insert cDe;

        newattachment_id = contentver.ContentDocumentId;
        newattachment_name = filename;
      } catch (Exception e) {
        System.debug(
          'Dashboard_Tab_Contract_Forms.doAttachmentLast() - Exception: ' +
          e.getMessage()
        );
      }
    }
    filename = null;
    body = null;
    getDocumentsByBid();
  }
  public void getDocumentsByBid() {
    documentBidList = new List<ContentDocument>();
    documentListPages = new List<Integer>();
    documentListFirst = 0;
    documentListPage = 1;
    documentListLastPage = 0;
    if (formBid != null && formBid.Id != null) {
      Set<String> contentDocumentIds = new Set<String>();
      for (ContentDocumentLink cdl : [
        SELECT Id, LinkedEntityId, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :formBid.Id
      ])
        contentDocumentIds.add(cdl.ContentDocumentId);
      documentBidList = [
        SELECT Id, Title, FileExtension, CreatedDate
        FROM ContentDocument
        WHERE Id IN :contentDocumentIds
        ORDER BY CreatedDate DESC
      ];
      if (!documentBidList.isEmpty()) {
        Integer i = 0;
        do {
          i++;
          documentListPages.add(i);
        } while ((i * 10) < documentBidList.size());
        documentListLastPage = i;
      }
    }
  }
  //End Attachs
  //Send Email
  public void sendEmail() {
    try {
      if (String.isNotBlank(formValue)) {
        saveBidAgreement();
        if (bidParentSObject == 'Air') {
          if (formValue == 'Form_Deposit_Due__c') {
            form_subject = form_subject.replace(
              '{ClientDueDate}',
              formBid.Client_Deposit_Due_Date__c != null
                ? Datetime.newInstance(
                      formBid.Client_Deposit_Due_Date__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
            form_body = form_body.replace(
              '{ClientDueDate}',
              formBid.Client_Deposit_Due_Date__c != null
                ? Datetime.newInstance(
                      formBid.Client_Deposit_Due_Date__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
          } else if (formValue == 'Form_Utilization__c') {
            form_subject = form_subject.replace(
              '{ClientDueDate}',
              formBid.Client_Utilization_Date__c != null
                ? Datetime.newInstance(
                      formBid.Client_Utilization_Date__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
            form_body = form_body.replace(
              '{ClientDueDate}',
              formBid.Client_Utilization_Date__c != null
                ? Datetime.newInstance(
                      formBid.Client_Utilization_Date__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
          } else if (formValue == 'Form_Names_Final_Payment__c') {
            form_subject = form_subject.replace(
              '{ClientDueDate}',
              formBid.Client_Names_Final_Payment__c != null
                ? Datetime.newInstance(
                      formBid.Client_Names_Final_Payment__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
            form_body = form_body.replace(
              '{ClientDueDate}',
              formBid.Client_Names_Final_Payment__c != null
                ? Datetime.newInstance(
                      formBid.Client_Names_Final_Payment__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('dd MMMMM yy')
                : ''
            );
          }
        }
        //Fix By Clay 29 Dec, 2020
        if (String.isNotBlank(form_closing)) {
        	form_body += '<p>' + form_closing.replaceAll('
|
|', '</p><p>') + '</p>';
        }
        send(
          form_to,
          form_cc,
          form_bcc,
          form_subject,
          form_body,
          form_attachs,
          bidAgreement_congaEmailFromId
        );
        Bid__c bid = new Bid__c(id = formBid.id);
        bid.put(
          formValue == 'Form_Credit_Card_Change__c'
            ? 'Credit_Card_Last_Send_Date__c'
            : formValue == 'Form_Cancellation_Letter__c'
                ? 'Cancellation_Last_Send_Date__c'
                : formValue == 'Form_Deposit_Due__c'
                    ? 'Deposit_Due_Last_Send_Date__c'
                    : formValue == 'Form_Utilization__c'
                        ? 'Utilization_Last_Send_Date__c'
                        : formValue == 'Form_Names_Final_Payment__c'
                            ? 'Names_Final_Payment_Last_Send_Date__c'
                            : formValue == 'Form_Final_Air_Confirmation__c'
                                ? 'Final_Air_Confirmation_Last_Send_Date__c'
                                : '',
          Datetime.now()
        );
        List<Task> tracesToUpdate = new List<Task>();
        if (bidParentSObject == 'Ground') {
          if (formValue == 'Form_Cancellation_Letter__c') {
            for (Task trace : [
              SELECT id, Subject, WhatId
              FROM Task
              WHERE
                WhatId = :formBid.id
                AND Contract_Task__c = TRUE
                AND Subject = 'Pending Cancellation'
            ]) {
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 1);
              trace.Status = 'Open';
              tracesToUpdate.add(trace);
            }
          }
          if (formValue == 'Form_Email_Confirmation__c') {
            if (
              String.isBlank(draft.Production_Assoc_Type__c) ||
              draft.Production_Assoc_Type__c == 'production_contacts'
            )
              for (Task trace : [
                SELECT id, Subject, WhatId
                FROM Task
                WHERE
                  WhatId = :formBid.id
                  AND Contract_Task__c = TRUE
                  AND Subject = 'Confirmation Email'
              ]) {
                trace.ActivityDate = null;
                trace.Status = 'Completed';
                tracesToUpdate.add(trace);
              }
          }
        }
        update bid;
        if (!tracesToUpdate.isEmpty())
          update tracesToUpdate;
        if (String.isNotEmpty(bidAgreementPrimaryContact.id))
          insert new Journal__c(
            RecordTypeId = journal_bidjournalRT,
            Bid__c = formBid.Id,
            Journal_Entry__c = formLabel +
              ' was sent to ' +
              bidAgreementPrimaryContact.get('Name') +
              ' ' +
              bidAgreementPrimaryContact.get('Email') +
              (String.isNotBlank(form_cc) ? ', cc: ' + form_cc : '') +
              (String.isNotBlank(form_bcc) ? ', bcc: ' + form_bcc : '')
          );
        else if (String.isNotEmpty(bidAgreementAttentionContact.id))
          insert new Journal__c(
            RecordTypeId = journal_bidjournalRT,
            Bid__c = formBid.Id,
            Journal_Entry__c = formLabel +
              ' was sent to ' +
              bidAgreementAttentionContact.Name +
              ' ' +
              bidAgreementAttentionContact.Email +
              (String.isNotBlank(form_cc) ? ', cc: ' + form_cc : '') +
              (String.isNotBlank(form_bcc) ? ', bcc: ' + form_bcc : '')
          );
      }
    } catch (Exception e) {
      System.debug(
        'Dashboard_Tab_Contract_Forms.sendEmail() - Exception: ' +
        e.getMessage()
      );
    }
  }
  public static String send(
    String toList,
    String ccList,
    String bccList,
    String subject,
    String body,
    String attachs,
    String emailFromId
  ) {
    try {
      //TO
      Set<String> toAddress = new Set<String>();
      for (String k : toList.split(','))
        if (k.trim() != '')
          toAddress.add(k.trim());
      //CC
      Set<String> ccAddress = new Set<String>();
      for (String k : ccList.split(','))
        if (k.trim() != '')
          ccAddress.add(k.trim());
      //BCC
      Set<String> bccAddress = new Set<String>();
      for (String k : bccList.split(','))
        if (k.trim() != '')
          bccAddress.add(k.trim());

      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
      if (String.isNotEmpty(emailFromId))
        mail.setOrgWideEmailAddressId(emailFromId);
      mail.setToAddresses(new List<String>(toAddress));
      if (ccAddress.size() > 0)
        mail.setCcAddresses(new List<String>(ccAddress));
      if (bccAddress.size() > 0)
        mail.setBccAddresses(new List<String>(bccAddress));
      mail.setSubject(subject);
      mail.setHtmlBody(body);

      if (attachs != null) {
        Set<String> attachIds = new Set<String>();
        for (String att : attachs.split(',')) {
          if (att.trim() != '')
            attachIds.add(att.trim());
        }
        //Attachment
        List<ContentVersion> contentVersions = [
          SELECT Id, ContentDocumentId, Title, PathOnClient, VersionData
          FROM ContentVersion
          WHERE ContentDocumentId IN :attachIds
        ];
        List<Messaging.Emailfileattachment> fileAttachments = new List<Messaging.Emailfileattachment>();
        if (contentVersions.size() > 0) {
          Messaging.Emailfileattachment efa;
          for (ContentVersion cv : contentVersions) {
            efa = new Messaging.Emailfileattachment();
            efa.setFileName(
              cv.PathOnClient.subString(2, cv.PathOnClient.length())
            );
            efa.setBody(cv.VersionData);
            fileAttachments.add(efa);
          }
        }
        if (fileAttachments.size() > 0)
          mail.setFileAttachments(fileAttachments);
      }
      myEmails.add(mail);
      Messaging.SendEmailResult[] mailResult = Messaging.sendEmail(myEmails);
      if (!mailResult[0].isSuccess())
        return mailResult[0].getErrors()[0].getMessage();
    } catch (System.EmailException e) {
      System.debug(
        '###Dashboard_Tab_Contract_Forms.send() - Email Exception: ' +
        e.getMessage()
      );
      return 'An internal error has occurred. Please contact your administrator.';
    }
    return '';
  }
  public static String verifyWideAddress(String email) {
    String oweaId;
    List<OrgWideEmailAddress> oweaList;
    if (Test.isRunningTest())
      oweaList = [
        SELECT Id
        FROM OrgWideEmailAddress
        WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c
      ];
    else
      oweaList = [SELECT Id FROM OrgWideEmailAddress WHERE Address = :email];
    if (oweaList.isEmpty())
      oweaList = [
        SELECT Id
        FROM OrgWideEmailAddress
        WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c
      ]; //Email default
    oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
    return oweaId;
  }
  public User verifyEmailUser(String userId) {
    Map<String, User> associationsMap = new Map<String, User>();
    List<Production_Associations__c> productAssociactions = [
      SELECT Id, User__c, User__r.Name, User__r.Email, User__r.Phone
      FROM Production_Associations__c
      WHERE
        RecordType.DeveloperName = 'Production_Coordinators'
        AND Production_Opp__c = :formBid.Production__c
        AND Team_Roles__c INCLUDES ('Primary Contract Coordinator')
        AND User__c != NULL
    ];
    return !productAssociactions.isEmpty() &&
      (productAssociactions[0].User__c == userId ||
      String.isEmpty(formBid.Contracting_Back_End_Coordinator__c))
      ? productAssociactions[0].User__r
      : String.isNotEmpty(formBid.Contracting_Back_End_Coordinator__c)
          ? formBid.Contracting_Back_End_Coordinator__r
          : new User();
  }
  //End Send Email
  //Wrappers
  public class FormWrapper {
    public String label { get; set; }
    public String value { get; set; }
    public String draftCode { get; set; }
    public FormWrapper(String label, String value, String draftCode) {
      this.label = label;
      this.value = value;
      this.draftCode = draftCode;
    }
  }
  public class wrapperData {
    public String data { get; set; }
    public String value { get; set; }
    public String extra1 { get; set; }
    public wrapperData(String data, String value, String extra1) {
      this.data = data;
      this.value = value;
      this.extra1 = extra1;
    }
  }
  public class GcqWrapper {
    public String gcqName { get; set; }
    public String tripId { get; set; }
    public String tripDescription { get; set; }
    public String bidId { get; set; }
    public Map<Air__c, List<Air__c>> itinerarySegmentsMap { get; set; }
    public Map<Air__c, List<Air__c>> deviationSegmentsMap { get; set; }
    public GcqWrapper(String gcqName) {
      this.gcqName = gcqName;
      itinerarySegmentsMap = new Map<Air__c, List<Air__c>>();
      deviationSegmentsMap = new Map<Air__c, List<Air__c>>();
    }
  }
  //End Wrappers
}```

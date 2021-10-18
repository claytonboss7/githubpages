---
layout: default
title: Dashboard_Tab_Contracting
parent: classes
---

```global class Dashboard_Tab_Contracting {
    public DashboardConfigurationWrapper vfpConfiguration {get;set;}
    public User user {get;set;}
    public Bid__c bidSelected {get;set;}
    public String bidId {get;set;}
    public String bidName {get;set;}
    public String parentId {get;set;}
    public Boolean isPageLoaded {get;set;}
    public Boolean loadTable {get;set;}
    public String orderFieldBidContract {get;set;}
    public String orderOrientationBidContract {get;set;}
    public Boolean isColumnSelected {get;set;}
    public Boolean isSortUpdated {get;set;}
    public String tabContractDefault {get;set;}
    public Map<Id,Contact> vendorContacts {get;set;}
    public List<SelectOption> vendorContactOptions {get;set;}
    public String contactClientValue {get;set;}
    public Map<String,AssociationWrapper> associations {get;set;}
    public Boolean loadDocuments {get;set;}
    public Date search_startdate {get;set;}
    public Date search_enddate {get;set;}
    public String search_vendor {get;set;}
    public String search_city {get;set;}
    public Boolean search_isprior {get;set;}
    public Boolean search_iscontracted {get;set;}
    public Boolean search_iscancelled {get;set;}
    public Ground__c groundFilter {get;set;}
    public List<SelectOption> teamMembers {get;set;}
    public String contractingbackendcoordinatorGT {get;set;}
    public String prod_assoc_CoordinatorsRT {get;set;}
    public String prod_assoc_ContactsRT {get;set;}
    public String contactContracting {get;set;}
    public String contractFinalStatus {get;set;}
    public Date trip_decisionduedate {get;set;}
    
    //Pagination
    public Integer limitContract {get;set;}
    public Integer offsetContract {get;set;}
    public Integer totalPagesContract {get;set;}
    public String searchTypeContract {get;set;}
    public Id firstId {get;set;}
    public Id lastId {get;set;}
    public Object firstValueOfSortedField {get;set;}
    public Object lastValueOfSortedField {get;set;}
    
    public final String CONTACT_CLIENT {
        set;
        get {
            if(CONTACT_CLIENT == null) CONTACT_CLIENT = 'client';
            return CONTACT_CLIENT;
        }
    }
    public final String USER_GTCOORDINATOR {
        set;
        get {
            if(USER_GTCOORDINATOR == null) USER_GTCOORDINATOR = 'gtCoordinator';
            return USER_GTCOORDINATOR;
        }
    }
    public final String USER_GTBACKENDCOORDINATOR {
        set;
        get {
            if(USER_GTBACKENDCOORDINATOR == null) USER_GTBACKENDCOORDINATOR = 'gtBackEndCoordinator';
            return USER_GTBACKENDCOORDINATOR;
        }
    }
    public final String USER_CONTRACTINGCOORDINATOR {
        set;
        get {
            if(USER_CONTRACTINGCOORDINATOR == null) USER_CONTRACTINGCOORDINATOR = 'contractingCoordinator';
            return USER_CONTRACTINGCOORDINATOR;
        }
    }
    public final String USER_CONTRACTINGBACKENDCOORDINATOR{
        set;
        get {
            if(USER_CONTRACTINGBACKENDCOORDINATOR == null) USER_CONTRACTINGBACKENDCOORDINATOR = 'contractingBackendCoordinator';
            return USER_CONTRACTINGBACKENDCOORDINATOR;
        }
    }
    public DashboardSearchBoxWrapper searchBoxWrapper {
        set;
        get {
            if(searchBoxWrapper == null) searchBoxWrapper = new DashboardSearchBoxWrapper();
            return searchBoxWrapper;
        }
    }
    public List<DashboardBidContractWrapper> bidContractsList {
        set;
        get {
            if(bidContractsList == null) bidContractsList = new List<DashboardBidContractWrapper>();
            return bidContractsList;
        }
    }
    public Map<Id,Bid__c> bidContractMap {get;set;}
    public List<SelectOption> bidContractStatusOptions {
        set;
        get {
            if(bidContractStatusOptions == null) {
                bidContractStatusOptions = new List<SelectOption>();
                //bidContractStatusOptions.add(new SelectOption('','All'));
                //for(Schema.PicklistEntry ple : Bid__c.Final_Status__c.getDescribe().getPicklistValues()) bidContractStatusOptions.add(new SelectOption(ple.getValue(),ple.getLabel()));
                bidContractStatusOptions.add(new SelectOption('','-- Select --'));
                bidContractStatusOptions.add(new SelectOption('Itinerary Received','Itinerary Received'));
                bidContractStatusOptions.add(new SelectOption('Bid Request Stage','Bid Request Stage'));
                bidContractStatusOptions.add(new SelectOption('Presenter/Promoter Provided','Presenter/Promoter Provided'));
                bidContractStatusOptions.add(new SelectOption('Pending Client Choice','Pending Client Choice'));
                bidContractStatusOptions.add(new SelectOption('Budgeting','Budgeting'));
                bidContractStatusOptions.add(new SelectOption('Cancelled','Cancelled'));
                bidContractStatusOptions.add(new SelectOption('Contracted on Own','Contracted on Own'));
                bidContractStatusOptions.add(new SelectOption('Layoff','Layoff'));
                bidContractStatusOptions.add(new SelectOption('Pending Trip Information','Pending Trip Information'));
                bidContractStatusOptions.add(new SelectOption('Pending Airport Confirmation','Pending Airport Confirmation'));
                bidContractStatusOptions.add(new SelectOption('Send to Client','Send to Client'));
            }
            return bidContractStatusOptions;
        }
    }
    
    public Dashboard_Tab_Contracting() {
        limitContract = 20;
        prod_assoc_CoordinatorsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Production_Associations__c' and DeveloperName = 'Production_Coordinators'].Id;
        prod_assoc_ContactsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Production_Associations__c' and DeveloperName = 'Production_Contacts'].Id;
        isPageLoaded = false;
        loadTable = true;
        
        groundFilter = new Ground__c();
        search_startdate = null;
        search_enddate = null;
        search_vendor = null;
        search_city = null;
        search_isprior = false;
        search_iscontracted = false;
        search_iscancelled = false;
        
        teamMembers = new List<SelectOption>();
        teamMembers.add(new SelectOption('','-- Not Assigned --'));
        Map<Id,Profile> profileIds = new Map<id,profile>([SELECT Id,UserLicenseId FROM Profile where UserLicenseId  in (SELECT Id FROM UserLicense where name ='Salesforce')]);
        for(User k1 : [SELECT Id, Name FROM User WHERE isActive = true AND ProfileId IN: profileIds.Keyset() ORDER BY Name ASC]) teamMembers.add(new SelectOption(k1.Id,k1.Name));
        associations = new Map<String,AssociationWrapper>{
            CONTACT_CLIENT  => new AssociationWrapper(),
            USER_GTCOORDINATOR => new AssociationWrapper(),
            USER_GTBACKENDCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGBACKENDCOORDINATOR => new AssociationWrapper()
        };
        User user = [Select id, Housing_Preference__c from User where id =:UserInfo.getUserId()];
    }
    
    public void loadBidContracts() {
        loadTable = false;
        searchBidContracts();
        system.debug(vfpConfiguration.bidId);
        if(!vfpConfiguration.bidId.equals('')) bidContracted();
    }
    
    public void changeFinalStatus(){
        searchBidContracts();
        if(bidSelected != null){
            bidSelected.Final_Status__c = contractFinalStatus;
            update bidSelected;
            switch on vfpConfiguration.parentSObject {
                when 'Housing' { update new Housing__c(Id = parentId, Status_CC__c = contractFinalStatus); }
                when 'Ground' { update new Ground__c(Id = parentId, Status_Ground__c = contractFinalStatus); }
                when 'Freight'{ update new Freight__c(Id = parentId, Status__c = contractFinalStatus); }
                when 'Air'{ update new Air__c(Id = parentId, Status__c = contractFinalStatus); }
            }
        }
    }
    
    public void changeContactContract(){
        if(bidSelected != null){
            bidSelected.Vendor_Contact__c = contactContracting;
            update bidSelected;
        }
    }
    
    public void changeClientContract(){
        if(contactClientValue != null && contactClientValue != ''){
            Contact clientByProduction = [SELECT Id, FirstName, Name, Phone, Email, Title, MobilePhone FROM Contact WHERE Id =: contactClientValue LIMIT 1];
            List<Production_Associations__c> paList = [SELECT Id, Contact__c, Role__c, Production_Opp__c FROM Production_Associations__c WHERE Production_Opp__c =: vfpConfiguration.productionId AND Contact__c <> NULL AND RecordType.DeveloperName = 'Production_Contacts'];
            system.debug(paList);
            if(paList.size() > 0){
                String roles;
                for(Production_Associations__c pAssoc : paList){
                    if(contactClientValue != null && contactClientValue != '' && pAssoc.Contact__c == contactClientValue && pAssoc.Role__c != null){
                        if(vfpConfiguration.parentSObject == 'Ground'){
                            if(pAssoc.Role__c != null && !pAssoc.Role__c.contains('Primary GT')){
                                pAssoc.Role__c = pAssoc.Role__c + ';Primary GT;';
                            }else{
                                if(pAssoc.Role__c == null) pAssoc.Role__c = 'Primary GT;';
                            }
                        }else if(vfpConfiguration.parentSObject == 'Freight'){
                            if(pAssoc.Role__c != null && !pAssoc.Role__c.contains('Primary Freight')){
                                pAssoc.Role__c = pAssoc.Role__c + ';Primary Freight;';
                            }else{
                                if(pAssoc.Role__c == null) pAssoc.Role__c = 'Primary Freight;';
                            }
                        }else if(vfpConfiguration.parentSObject == 'Air'){
                            if(pAssoc.Role__c != null && !pAssoc.Role__c.contains('Primary Air')){
                                pAssoc.Role__c = pAssoc.Role__c + ';Primary Air;';
                            }else{
                                if(pAssoc.Role__c == null) pAssoc.Role__c = 'Primary Air;';
                            }
                        }
                    }else{
                        roles = '';
                        if(pAssoc.Role__c != null){
                            for(String tr : pAssoc.Role__c.split(';')){
                                if(vfpConfiguration.parentSObject == 'Ground' && tr != 'Primary GT') roles = roles + tr + ';';
                                if(vfpConfiguration.parentSObject == 'Freight' && tr != 'Primary Freight') roles = roles + tr + ';';
                                if(vfpConfiguration.parentSObject == 'Air' && tr != 'Primary Air') roles = roles + tr + ';';
                            }
                        }
                        pAssoc.Role__c = roles;
                    }
                }
                system.debug(paList);
                update paList;
            }else{
                if(vfpConfiguration.parentSObject == 'Ground') insert new Production_Associations__c(RecordTypeId = prod_assoc_ContactsRT, Production_Opp__c = vfpConfiguration.productionId,Role__c = 'Primary GT;', Contact__c = contactClientValue);
                if(vfpConfiguration.parentSObject == 'Freight') insert new Production_Associations__c(RecordTypeId = prod_assoc_ContactsRT, Production_Opp__c = vfpConfiguration.productionId,Role__c = 'Primary Freight;', Contact__c = contactClientValue);
                if(vfpConfiguration.parentSObject == 'Air') insert new Production_Associations__c(RecordTypeId = prod_assoc_ContactsRT, Production_Opp__c = vfpConfiguration.productionId,Role__c = 'Primary Air;', Contact__c = contactClientValue);
            }
        }
    }
    
    public void saveContractingBackEndCoordinator(){
        if(bidSelected != null){
            bidSelected.Contracting_Back_End_Coordinator__c = !String.isEmpty(contractingbackendcoordinatorGT) ? contractingbackendcoordinatorGT : null;
            update bidSelected;
        }
    }
    
    public void searchBidContracts() {
        bidContractsList.clear();
        system.debug('bid id: ' +vfpConfiguration.bidId);
        if(vfpConfiguration != null) {
            System.debug('VFP CONFIGURATION');
            System.debug('vfpConfiguration.productionParentId -> '+vfpConfiguration.productionParentId);
            System.debug('vfpConfiguration.productionId -> '+vfpConfiguration.productionId);
            System.debug('vfpConfiguration.productionName -> '+vfpConfiguration.productionName);
            System.debug('vfpConfiguration.parentSObject -> '+vfpConfiguration.parentSObject);
            System.debug('vfpConfiguration.parentId -> '+vfpConfiguration.parentId);
            System.debug('vfpConfiguration.bidId -> '+vfpConfiguration.bidId);
            System.debug('vfpConfiguration.bidStatus -> '+vfpConfiguration.bidStatus);
        }
        DashboardBidContractWrapper.orderFieldBidContract = orderFieldBidContract;
        
        String orderFieldBidContractAux;
        Date tdy = system.today();
        bidContractMap = new Map<Id,Bid__c>();
        Map<String,Ground__c> groundMap = new Map<String,Ground__c>();
        String strQuery = 'SELECT Id, Name, Vendor__c, Vendor__r.Name, Vendor__r.ParentId, Vendor_Contact__c, Status__c, Provider__c,';
        system.debug(vfpConfiguration.parentSObject);
        system.debug(search_isprior);
        system.debug(search_startdate);
        switch on vfpConfiguration.parentSObject {
            when 'Housing' {
                orderFieldBidContractAux = 'Housing__r.Date_In__c';
                strQuery += ' Housing__c, Housing__r.Date_In__c, Housing__r.Date_Out__c, Housing__r.Group__c, Venue__c, Venue__r.Name, City__c, City__r.Name FROM Bid__c WHERE Housing__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\'';
                if(search_startdate != null && search_enddate != null){
                    if(search_startdate == search_enddate){
                        strQuery += ' AND (Housing__r.Date_In__c <=: search_enddate AND Housing__r.Date_Out__c >=: search_enddate)';
                    }else{
                        strQuery += ' AND ((Housing__r.Date_In__c <=: search_startdate AND Housing__r.Date_Out__c >=: search_startdate) OR (Housing__r.Date_In__c <=: search_enddate AND Housing__r.Date_Out__c >=: search_enddate))';
                    }
                }else{
                    if(search_startdate != null) strQuery += ' AND (Housing__r.Date_In__c >=: search_startdate OR Housing__r.Date_Out__c >=: search_startdate)';
                    if(search_enddate != null) strQuery += ' AND (Housing__r.Date_In__c >=: search_enddate OR Housing__r.Date_Out__c <=: search_enddate)';
                }
                if(search_iscontracted) strQuery += ' AND Housing__r.Status__c = \'Contracted On Own\'';
            }
            when 'Ground' {
                orderFieldBidContractAux = 'GT__r.Start_Date__c';
                strQuery += ' GT__c, GT__r.Start_Date__c, GT__r.End_Date__c, GT__r.Group_Type__c, GT__r.Description__c, GT__r.Service_Type__c, GT__r.Service_Type_Text__c FROM Bid__c WHERE GT__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\'';
                system.debug(search_isprior);
                system.debug(search_startdate);
                if(!search_isprior){
                    if(search_startdate == null && search_enddate == null){
                        strQuery += ' AND GT__r.Start_Date__c >=: tdy';
                    }else{
                        if(search_startdate != null && search_enddate != null){
                            if(search_startdate == search_enddate){
                                strQuery += ' AND (GT__r.Start_Date__c <=: search_enddate AND GT__r.End_Date__c >=: search_enddate)';
                            }else{
                                strQuery += ' AND ((GT__r.Start_Date__c <=: search_startdate AND GT__r.End_Date__c >=: search_startdate) OR (GT__r.Start_Date__c <=: search_enddate AND GT__r.End_Date__c >=: search_enddate))';
                            }
                        }else{
                            if(search_startdate != null) strQuery += ' AND (GT__r.Start_Date__c >=: search_startdate OR GT__r.End_Date__c >=: search_startdate)';
                            if(search_enddate != null) strQuery += ' AND (GT__r.Start_Date__c >=: search_enddate OR GT__r.End_Date__c <=: search_enddate)';
                        }
                    }
                }
                if(search_iscontracted) strQuery += ' AND GT__r.Status_Ground__c = \'Contracted On Own\'';
            }
            when 'Freight' {
                orderFieldBidContractAux = 'Freight__r.Start_Date__c';
                strQuery += ' Freight__c, Freight__r.Start_Date__c, Freight__r.End_Date__c, Freight__r.Group_Type__c, Freight__r.Description__c, Freight__r.Service_Type__c FROM Bid__c WHERE Freight__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\'';
                if(!search_isprior){
                    if(search_startdate == null && search_enddate == null){
                        strQuery += ' AND Freight__r.Start_Date__c >=: tdy';
                    }else{
                        if(search_startdate != null && search_enddate != null){
                            if(search_startdate == search_enddate){
                                strQuery += ' AND (Freight__r.Start_Date__c <=: search_enddate AND Freight__r.End_Date__c >=: search_enddate)';
                            }else{
                                strQuery += ' AND ((Freight__r.Start_Date__c <=: search_startdate AND Freight__r.End_Date__c >=: search_startdate) OR (Freight__r.Start_Date__c <=: search_enddate AND Freight__r.End_Date__c >=: search_enddate))';
                            }
                        }else{
                            if(search_startdate != null) strQuery += ' AND (Freight__r.Start_Date__c >=: search_startdate OR Freight__r.End_Date__c >=: search_startdate)';
                            if(search_enddate != null) strQuery += ' AND (Freight__r.Start_Date__c >=: search_enddate OR Freight__r.End_Date__c <=: search_enddate)';
                        }
                    }
                }
                if(search_iscontracted) strQuery += ' AND Freight__r.Status__c = \'Contracted On Own\'';
            }
            when 'Air' {
                orderFieldBidContractAux = 'Air__r.Departure_Date__c';
                strQuery += ' Air__c, Air__r.Dep_Arr__c, Air__r.RT_Dep_Arr__c, Air__r.Decision_Due_Date__c, Air__r.Departure_Date__c, Air__r.Departure_City__r.Airport_Code__c, Air__r.Arrival_Date__c, Air__r.Arrival_City__r.Airport_Code__c, Air__r.Return_Date__c, Air__r.Return_Departure_City__c, Air__r.Return_Departure_City__r.Airport_Code__c, Air__r.Return_Arrival_City__c, Air__r.Return_Arrival_City__r.Airport_Code__c, Air__r.Trip_Type__c, Air__r.PAX__c, Air__r.Description__c FROM Bid__c WHERE Air__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\'';
                if(!search_isprior){
                    if(search_startdate == null && search_enddate == null){
                        strQuery += ' AND Air__r.Departure_Date__c >=: tdy';
                    }else{
                        if(search_startdate != null && search_enddate != null){
                            if(search_startdate == search_enddate){
                                strQuery += ' AND (Air__r.Departure_Date__c <=: search_enddate AND Air__r.Return_Date__c >=: search_enddate)';
                            }else{
                                strQuery += ' AND ((Air__r.Departure_Date__c <=: search_startdate AND Air__r.Return_Date__c >=: search_startdate) OR (Air__r.Departure_Date__c <=: search_enddate AND Air__r.Return_Date__c >=: search_enddate))';
                            }
                        }else{
                            if(search_startdate != null) strQuery += ' AND (Air__r.Departure_Date__c >=: search_startdate OR Air__r.Return_Date__c >=: search_startdate)';
                            if(search_enddate != null) strQuery += ' AND (Air__r.Departure_Date__c >=: search_enddate OR Air__r.Return_Date__c <=: search_enddate)';
                        }
                    }
                }
                if(search_iscontracted) strQuery += ' AND Air__r.Status__c = \'Contracted On Own\'';
            }
        }
        if(String.isNotBlank(search_vendor)){
            search_vendor = '%' + search_vendor.trim() + '%';
            strQuery += ' AND Vendor__r.Name LIKE: search_vendor';
        }
        if(String.isNotBlank(search_city)){
            search_city = '%' + search_city.trim()+ '%';
            if(vfpConfiguration.parentSObject == 'Air'){
                List<String> searchSplit = search_city.split(' - ');
                String str1;
                String str2;
                String str3;
                if(searchSplit.size() > 0){
                    if(searchSplit.size() == 3){
                        str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                        str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                        str3 = searchSplit[2] != null ? '%' + searchSplit[2].trim() + '%' : '%%';
                        strQuery += ' AND ((Air__r.Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Departure_City__r.Name LIKE: str2 OR Air__r.Departure_City__r.City__r.Name LIKE: str3)';
                        strQuery += ' OR (Air__r.Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Arrival_City__r.Name LIKE: str2 OR Air__r.Arrival_City__r.City__r.Name LIKE: str3)';
                        strQuery += ' OR (Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Arrival_City__r.Name LIKE: str2 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str3)';
                        strQuery += ' OR (Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Departure_City__r.Name LIKE: str2 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str3))';
                    }else if(searchSplit.size() == 2){
                        str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                        str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                        strQuery += ' AND (Air__r.Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Departure_City__r.Name LIKE: str1 OR Air__r.Departure_City__r.City__r.Name LIKE: str1 OR Air__r.Departure_City__r.Airport_Code__c LIKE: str2 OR Air__r.Departure_City__r.Name LIKE: str2 OR Air__r.Departure_City__r.City__r.Name LIKE: str2 '+
                            'OR Air__r.Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Arrival_City__r.Name LIKE: str1 OR Air__r.Arrival_City__r.City__r.Name LIKE: str1 OR Air__r.Arrival_City__r.Airport_Code__c LIKE: str2 OR Air__r.Arrival_City__r.Name LIKE: str2 OR Air__r.Arrival_City__r.City__r.Name LIKE: str2 ' +
                            'OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Arrival_City__r.Name LIKE: str1 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str1 OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str2 OR Air__r.Return_Arrival_City__r.Name LIKE: str2 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str2 ' +
                            'OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Departure_City__r.Name LIKE: str1 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str1 OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str2 OR Air__r.Return_Departure_City__r.Name LIKE: str2 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str2 ' +
                            ')';
                    }else{
                        search_city = '%' +  search_city + '%';
                        strQuery += ' AND (Air__r.Departure_City__r.Name LIKE: search_city OR Air__r.Departure_City__r.Airport_Code__c LIKE: search_city ' +
                            'OR Air__r.Arrival_City__r.Name LIKE: search_city OR Air__r.Arrival_City__r.Airport_Code__c LIKE: search_city ' +
                            'OR Air__r.Return_Arrival_City__r.Name LIKE: search_city OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: search_city ' +
                            'OR Air__r.Return_Departure_City__r.Name LIKE: search_city OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: search_city ' +
                            ')';
                    }
                }else{
                    search_city = '%' +  search_city + '%';
                    strQuery += ' AND (Air__r.Departure_City__r.Name LIKE: search_city OR Air__r.Departure_City__r.Airport_Code__c LIKE: search_city ' +
                        'OR Air__r.Arrival_City__r.Name LIKE: search_city OR Air__r.Arrival_City__r.Airport_Code__c LIKE: search_city ' +
                        'OR Air__r.Return_Arrival_City__r.Name LIKE: search_city OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: search_city ' +
                        'OR Air__r.Return_Departure_City__r.Name LIKE: search_city OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: search_city ' +
                        ')';
                }
            } 
            else strQuery += ' AND City__r.Name LIKE: search_city';
        }
        //if(String.isNotBlank(vfpConfiguration.productionParentId) && search_isprior) strQuery += ' AND Production__c = \''+vfpConfiguration.productionParentId+'\'';
        //else strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\'';
        strQuery += search_iscancelled ? ' AND Status__c IN (\'Contracted\',\'Cancelled\')' : ' AND Status__c = \'Contracted\'';
        
        isColumnSelected = isColumnSelected == null ? false : isColumnSelected;
        isSortUpdated = isSortUpdated == null ? false : isSortUpdated;
        if(isColumnSelected){
            if(isSortUpdated) orderOrientationBidContract = 'ASC';
            else{
                if(orderOrientationBidContract == 'ASC') orderOrientationBidContract = 'DESC'; 
                else orderOrientationBidContract = 'ASC';
            }
        }
        isColumnSelected = false;
        
        Integer totalRecordsContract = Database.countQuery('Select count() from Bid__c WHERE' + strQuery.substringAfter('WHERE'));
        totalPagesContract = totalRecordsContract != null && totalRecordsContract == 0 ? 1 : Integer.valueOf((totalRecordsContract/Decimal.valueOf(limitContract)).round(System.RoundingMode.UP));
        List<Bid__c> bidList = new List<Bid__c>();
        orderOrientationBidContract = (orderOrientationBidContract != null && orderOrientationBidContract != '' ? orderOrientationBidContract : 'ASC');
        orderFieldBidContract = (orderFieldBidContract != null && orderFieldBidContract != '' ? orderFieldBidContract : orderFieldBidContractAux);
        if(String.isBlank(searchTypeContract)){
            strQuery += ' ORDER BY ' + orderFieldBidContract + ' ' + orderOrientationBidContract + ' NULLS LAST' + ', Id LIMIT :limitContract';
            bidList = Database.query(strQuery);
            offsetContract = null;
        }
        else{
            if(searchTypeContract == 'next'){
                offsetContract = (offsetContract != null ? offsetContract : 0) + limitContract;
                strQuery += ' AND (' + orderFieldBidContract + (orderOrientationBidContract == 'ASC' ? ' >' : ' <') + ':lastValueOfSortedField OR (' + orderFieldBidContract  + ' =:lastValueOfSortedField AND Id >:lastId)) ORDER BY ' + orderFieldBidContract + ' ' + orderOrientationBidContract + ' NULLS LAST' + ', Id LIMIT :limitContract';
                bidList = Database.query(strQuery);
            }
            else if(searchTypeContract == 'previous'){
                offsetContract = (offsetContract != null ? offsetContract : 0) - limitContract;
                strQuery += ' AND (' + orderFieldBidContract + (orderOrientationBidContract == 'ASC' ? ' <' : ' >') + ':firstValueOfSortedField OR (' + orderFieldBidContract  + ' =:firstValueOfSortedField AND Id <:firstId)) ORDER BY ' + orderFieldBidContract + ' ' + (orderOrientationBidContract == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT :limitContract';
                bidList = Database.query(strQuery);
                List<Bid__c> airBids = new List<Bid__c>();
                for(Integer i = bidList.size() - 1; i >= 0; i--) airBids.add(bidList[i]);
                bidList = airBids;
            } 
            else if(searchTypeContract == 'first'){
                offsetContract = null;
                strQuery += ' ORDER BY ' + orderFieldBidContract + ' ' + orderOrientationBidContract + ' NULLS LAST' + ', Id LIMIT :limitContract';
                bidList = Database.query(strQuery);
            } 
            else if(searchTypeContract == 'last'){
                offsetContract = limitContract * (Integer.valueOf((totalRecordsContract / Decimal.valueOf(limitContract)).round(System.RoundingMode.CEILING)) - 1);
                strQuery += ' ORDER BY ' + orderFieldBidContract + ' ' + (orderOrientationBidContract == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT ' + String.valueOf(totalRecordsContract - offsetContract);
                bidList = Database.query(strQuery);
                List<Bid__c> airBids = new List<Bid__c>();
                for(Integer i = bidList.size() - 1; i >= 0; i--) airBids.add(bidList[i]);
                bidList = airBids;
            } 
        }
        firstId = !bidList.isEmpty() ? bidList[0].Id : null;
        lastId = !bidList.isEmpty() ? bidList[bidList.size() - 1].Id : null;
        firstValueOfSortedField = null;
        lastValueOfSortedField = null;
        if(!bidList.isEmpty()){
            switch on vfpConfiguration.parentSObject {
                when 'Housing' {
                    if(orderFieldBidContract == 'Housing__r.Date_In__c'){ firstValueOfSortedField = bidList[0].Housing__r.Date_In__c; lastValueOfSortedField = bidList[bidList.size() - 1].Housing__r.Date_In__c;
                    } else if(orderFieldBidContract == 'Housing__r.Date_Out__c'){ firstValueOfSortedField = bidList[0].Housing__r.Date_Out__c; lastValueOfSortedField = bidList[bidList.size() - 1].Housing__r.Date_Out__c;
                    } else if(orderFieldBidContract == 'Venue__r.Name'){ firstValueOfSortedField = bidList[0].Venue__r.Name; lastValueOfSortedField = bidList[bidList.size() - 1].Venue__r.Name;
                    } else if(orderFieldBidContract == 'City__r.Name'){ firstValueOfSortedField = bidList[0].City__r.Name; lastValueOfSortedField = bidList[bidList.size() - 1].City__r.Name;
                    } else if(orderFieldBidContract == 'Housing__r.Group__c'){ firstValueOfSortedField = bidList[0].Housing__r.Group__c; lastValueOfSortedField = bidList[bidList.size() - 1].Housing__r.Group__c;
                    } else{ firstValueOfSortedField = bidList[0].get(orderFieldBidContract); lastValueOfSortedField = bidList[bidList.size() - 1].get(orderFieldBidContract);}
                }
                when 'Ground' {
                    if(orderFieldBidContract == 'Vendor__r.Name'){ firstValueOfSortedField = bidList[0].Vendor__r.Name; lastValueOfSortedField = bidList[bidList.size() - 1].Vendor__r.Name;
                    } else if(orderFieldBidContract == 'GT__r.Start_Date__c'){ firstValueOfSortedField = bidList[0].GT__r.Start_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].GT__r.Start_Date__c;
                    } else if(orderFieldBidContract == 'GT__r.End_Date__c'){ firstValueOfSortedField = bidList[0].GT__r.End_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].GT__r.End_Date__c;
                    }else if(orderFieldBidContract == 'GT__r.Group_Type__c'){ firstValueOfSortedField = bidList[0].GT__r.Group_Type__c; lastValueOfSortedField = bidList[bidList.size() - 1].GT__r.Group_Type__c;
                    } else if(orderFieldBidContract == 'GT__r.Description__c'){ firstValueOfSortedField = bidList[0].GT__r.Description__c; lastValueOfSortedField = bidList[bidList.size() - 1].GT__r.Description__c;
                    } else if(orderFieldBidContract == 'GT__r.Service_Type_Text__c'){ firstValueOfSortedField = bidList[0].GT__r.Service_Type_Text__c; lastValueOfSortedField = bidList[bidList.size() - 1].GT__r.Service_Type_Text__c;
                    } else{ firstValueOfSortedField = bidList[0].get(orderFieldBidContract); lastValueOfSortedField = bidList[bidList.size() - 1].get(orderFieldBidContract); }
                }
                when 'Freight'{
                    if(orderFieldBidContract == 'Vendor__r.Name'){ firstValueOfSortedField = bidList[0].Vendor__r.Name; lastValueOfSortedField = bidList[bidList.size() - 1].Vendor__r.Name;
                    } else if(orderFieldBidContract == 'Freight__r.Start_Date__c'){ firstValueOfSortedField = bidList[0].Freight__r.Start_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].Freight__r.Start_Date__c;
                    } else if(orderFieldBidContract == 'Freight__r.End_Date__c'){ firstValueOfSortedField = bidList[0].Freight__r.End_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].Freight__r.End_Date__c;
                    }else if(orderFieldBidContract == 'Freight__r.Group_Type__c'){ firstValueOfSortedField = bidList[0].Freight__r.Group_Type__c; lastValueOfSortedField = bidList[bidList.size() - 1].Freight__r.Group_Type__c;
                    } else if(orderFieldBidContract == 'Freight__r.Description__c'){ firstValueOfSortedField = bidList[0].Freight__r.Description__c; lastValueOfSortedField = bidList[bidList.size() - 1].Freight__r.Description__c;
                    } else if(orderFieldBidContract == 'Freight__r.Service_Type__c'){ firstValueOfSortedField = bidList[0].Freight__r.Service_Type__c; lastValueOfSortedField = bidList[bidList.size() - 1].Freight__r.Service_Type__c;
                    } else{ firstValueOfSortedField = bidList[0].get(orderFieldBidContract); lastValueOfSortedField = bidList[bidList.size() - 1].get(orderFieldBidContract); }
                }
                when 'Air'{
                    if(orderFieldBidContract == 'Vendor__r.Name'){ firstValueOfSortedField = bidList[0].Vendor__r.Name; lastValueOfSortedField = bidList[bidList.size() - 1].Vendor__r.Name;
                    } else if(orderFieldBidContract == 'Air__r.Departure_Date__c'){ firstValueOfSortedField = bidList[0].Air__r.Departure_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.Departure_Date__c;
                    } else if(orderFieldBidContract == 'Air__r.Return_Date__c'){ firstValueOfSortedField = bidList[0].Air__r.Return_Date__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.Return_Date__c;
                    }else if(orderFieldBidContract == 'Air__r.Trip_Type__c'){ firstValueOfSortedField = bidList[0].Air__r.Trip_Type__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.Trip_Type__c;
                    } else if(orderFieldBidContract == 'Air__r.PAX__c'){ firstValueOfSortedField = bidList[0].Air__r.PAX__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.PAX__c;
                    } else if(orderFieldBidContract == 'Air__r.Dep_Arr__c'){ firstValueOfSortedField = bidList[0].Air__r.Dep_Arr__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.Dep_Arr__c;
                    } else if(orderFieldBidContract == 'Air__r.RT_Dep_Arr__c'){ firstValueOfSortedField = bidList[0].Air__r.RT_Dep_Arr__c; lastValueOfSortedField = bidList[bidList.size() - 1].Air__r.RT_Dep_Arr__c;
                    } else{ firstValueOfSortedField = bidList[0].get(orderFieldBidContract); lastValueOfSortedField = bidList[bidList.size() - 1].get(orderFieldBidContract); }
                }
            }
        }
        searchTypeContract = null;
        
        for(Bid__c b : bidList) bidContractMap.put(b.Id,b);
        bidList = null;
        for(Bid__c b : bidContractMap.values()) {
            DashboardBidContractWrapper bidContract;
            switch on vfpConfiguration.parentSObject {
                when 'Housing'{ 
                    bidContract = new DashboardBidContractWrapper(b.Id, b.Name, b.Vendor__r.Name, b.Vendor__c, b.Status__c);
                    bidContract.setHousingFields(b.Housing__c, b.Housing__r.Date_In__c, b.Housing__r.Date_Out__c, b.Venue__r.Name, b.City__r.Name, b.Housing__r.Group__c); 
                }
                when 'Ground' {
                    bidContract = new DashboardBidContractWrapper(b.GT__r, b.Id, b.Name, b.Vendor__r.Name, b.Vendor__c, b.Status__c);
                    bidContract.setGroundFields(b.GT__c, b.GT__r.Start_Date__c, b.GT__r.End_Date__c, b.GT__r.Group_Type__c, b.GT__r.Description__c, b.GT__r.Service_Type_Text__c);
                }
                when 'Freight'{
                    bidContract = new DashboardBidContractWrapper(b.Freight__r, b.Id, b.Name, b.Vendor__r.Name, b.Vendor__c, b.Status__c);
                    bidContract.setFreightFields(b.Freight__c, b.Freight__r.Start_Date__c, b.Freight__r.End_Date__c, b.Freight__r.Group_Type__c, b.Freight__r.Description__c, b.Freight__r.Service_Type__c);
                }
                when 'Air'{
                    bidContract = new DashboardBidContractWrapper(b.Air__r, b.Id, b.Name, b.Vendor__r.Name, b.Vendor__c, b.Status__c);
                    bidContract.setAirFields(b.Air__c, b.Air__r.Departure_Date__c, b.Air__r.Dep_Arr__c, b.Air__r.Return_Date__c, b.Air__r.RT_Dep_Arr__c, b.Air__r.Trip_Type__c, String.valueOf(b.Air__r.PAX__c));
                }
            }
            bidContractsList.add(bidContract);
        }
        
        contactClientValue = '';
        associations = new Map<String,AssociationWrapper>{
            CONTACT_CLIENT  => new AssociationWrapper(),
            USER_GTCOORDINATOR => new AssociationWrapper(),
            USER_GTBACKENDCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGBACKENDCOORDINATOR => new AssociationWrapper()
        };
        system.debug('bid id: ' +vfpConfiguration.bidId);
    }
    
    public void saveDecisionDue(){
        if(bidSelected != null && bidSelected.Air__c != null){
            update new Air__c(Id = bidSelected.Air__c,Decision_Due_Date__c = trip_decisionduedate);
        }
    }
    
    public void viewBidContracted() {
        //if(bidContractMap.containsKey(bidId)) {
        if(bidId != null && bidId != '') {
            vfpConfiguration.bidId = bidId;
            vfpConfiguration.bidName = bidName;
            vfpConfiguration.parentId = parentId;
            bidContracted();
        } else {
            bidId = '';
            parentId = '';
            tabContractDefault = '';
        }
    }
    
    public static Bid__c getBidInformation(DashboardConfigurationWrapper vfpConfiguration){
        system.debug ('inside this getBidInformation method :: ' + vfpConfiguration);
        Bid__c selectBid;
        String strQuery = 'SELECT Id, Name, Contracting_Back_End_Coordinator__c, Contracting_Back_End_Coordinator__r.Name, Vendor__c, Vendor__r.Name, Vendor__r.ParentId, Vendor_Contact__c, Status__c, Provider__c,';
        switch on vfpConfiguration.parentSObject {
            when 'Housing' {
                strQuery += ' Housing__c, Housing__r.Date_In__c, Housing__r.Date_Out__c, Housing__r.Group__c, Venue__c, Venue__r.Name, City__c, City__r.Name FROM Bid__c WHERE Housing__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\' AND Id = \''+vfpConfiguration.bidId+'\'';
            }
            when 'Ground' {
                strQuery += ' GT__c, GT__r.Start_Date__c, GT__r.End_Date__c, GT__r.Group_Type__c, GT__r.Description__c, GT__r.Service_Type__c FROM Bid__c WHERE GT__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\' AND Id = \''+vfpConfiguration.bidId+'\'';
            }
            when 'Freight' {
                strQuery += ' Freight__c, Freight__r.Start_Date__c, Freight__r.End_Date__c, Freight__r.Group_Type__c, Freight__r.Description__c, Freight__r.Service_Type__c FROM Bid__c WHERE Freight__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\' AND Id = \''+vfpConfiguration.bidId+'\'';
            }
            when 'Air' {
                strQuery += ' Air__c, Air__r.Decision_Due_Date__c, Air__r.Departure_Date__c, Air__r.Departure_City__r.Airport_Code__c, Air__r.Arrival_Date__c, Air__r.Arrival_City__r.Airport_Code__c, Air__r.Return_Date__c, Air__r.Return_Departure_City__c, Air__r.Return_Departure_City__r.Airport_Code__c, Air__r.Return_Arrival_City__c, Air__r.Return_Arrival_City__r.Airport_Code__c, Air__r.Trip_Type__c, Air__r.PAX__c, Air__r.Description__c FROM Bid__c WHERE Air__c != null';
                strQuery += ' AND Production__c = \''+vfpConfiguration.productionId+'\' AND Id = \''+vfpConfiguration.bidId+'\'';
            }
        }
        for(Bid__c b : Database.query(strQuery)) selectBid = b;
        return selectBid;
    }
    public void bidContracted() {
        system.debug(bidContractMap);
        //if(bidContractMap.containsKey(vfpConfiguration.bidId)) {
        if(vfpConfiguration.bidId != null) {
            bidSelected = getBidInformation(vfpConfiguration);
            if(bidSelected != null && bidSelected.Status__c == 'Contracted' || bidSelected.Status__c == 'In Contracting' || bidSelected.Status__c == 'Pending Client Signature') {
                system.debug('exist in map contracted');
                //bidSelected = bidContractMap.get(vfpConfiguration.bidId);
                vfpConfiguration.bidStatus = bidSelected.Status__c;
                tabContractDefault = 'status';
                bidContractedGTAssociations();
            }else{
                system.debug('does not exist in map contracted');
                vfpConfiguration.bidId = '';
                vfpConfiguration.bidStatus = '';
                vfpConfiguration.parentId = '';
                tabContractDefault = '';
            }
        } else {
            system.debug('does not exist in map contracted');
            vfpConfiguration.bidId = '';
            vfpConfiguration.bidStatus = '';
            vfpConfiguration.parentId = '';
            tabContractDefault = '';
        }
        System.debug('bidContractId -> '+vfpConfiguration.bidId);
        System.debug('bidParentId -> '+vfpConfiguration.parentId);
        System.debug('bidParentSObject -> '+vfpConfiguration.parentSObject);
    }
    
    public void bidContractedGTAssociations() {
        associations = new Map<String,AssociationWrapper>{
            CONTACT_CLIENT  => new AssociationWrapper(),
            USER_GTCOORDINATOR => new AssociationWrapper(),
            USER_GTBACKENDCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGCOORDINATOR => new AssociationWrapper(),
            USER_CONTRACTINGBACKENDCOORDINATOR => new AssociationWrapper()
        };
        for(Production_Associations__c pa : [SELECT Id, User__c, User__r.Name, Team_Roles__c, Contact__c, Contact__r.Name, Role__c, Production_Opp__c FROM Production_Associations__c WHERE Production_Opp__c = :vfpConfiguration.productionId AND (User__c <> null OR Contact__c <> null)]){
            if(vfpConfiguration.parentSObject == 'Ground'){
                if(String.isBlank(associations.get(CONTACT_CLIENT).associationId) && pa.Role__c != null && pa.Role__c.contains('Primary GT')) associations.put(CONTACT_CLIENT, new AssociationWrapper(pa.Id, pa.Contact__c, pa.Contact__r.Name, pa.Role__c, 'Contact'));
                if(String.isBlank(associations.get(USER_GTCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Primary GT Coordinator')) associations.put(USER_GTCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
                //if(String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Ground Travel back-end Coordinator')) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
            }else if(vfpConfiguration.parentSObject == 'Freight'){
                if(String.isBlank(associations.get(CONTACT_CLIENT).associationId) && pa.Role__c != null && pa.Role__c.contains('Primary Freight')) associations.put(CONTACT_CLIENT, new AssociationWrapper(pa.Id, pa.Contact__c, pa.Contact__r.Name, pa.Role__c, 'Contact'));
                if(String.isBlank(associations.get(USER_GTCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Primary Freight Coordinator')) associations.put(USER_GTCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
                //if(String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Freight back-end Coordinator')) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
            }else if(vfpConfiguration.parentSObject == 'Air'){
                if(String.isBlank(associations.get(CONTACT_CLIENT).associationId) && pa.Role__c != null && pa.Role__c.contains('Primary Air')) associations.put(CONTACT_CLIENT, new AssociationWrapper(pa.Id, pa.Contact__c, pa.Contact__r.Name, pa.Role__c, 'Contact'));
                if(String.isBlank(associations.get(USER_GTCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Primary Air Coordinator')) associations.put(USER_GTCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
                //if(String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Air back-end Coordinator')) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
            }
            if(String.isBlank(associations.get(USER_CONTRACTINGCOORDINATOR).associationId) && pa.Team_Roles__c != null && pa.Team_Roles__c.contains('Primary Contract Coordinator')) associations.put(USER_CONTRACTINGCOORDINATOR, new AssociationWrapper(pa.Id, pa.User__c, pa.User__r.Name, pa.Team_Roles__c, 'User'));
            if(String.isBlank(associations.get(USER_CONTRACTINGBACKENDCOORDINATOR).associationId) && String.isNotEmpty(bidSelected.Contracting_Back_End_Coordinator__c)) associations.put(USER_CONTRACTINGBACKENDCOORDINATOR, new AssociationWrapper(pa.Id, bidSelected.Contracting_Back_End_Coordinator__c, bidSelected.Contracting_Back_End_Coordinator__r.Name, 'Contracting Back-End Coordinator', 'User'));
        }

        if(vfpConfiguration.parentSObject == 'Ground'){
            List<Ground__c> serviceAux = [SELECT Id, Back_end_Coordinator__c, Back_end_Coordinator__r.Name FROM Ground__c WHERE Id = :vfpConfiguration.parentId];
            if(!serviceAux.isEmpty() && String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && serviceAux[0].Back_end_Coordinator__c != null) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__r.Name,null, 'User'));
        }else if(vfpConfiguration.parentSObject == 'Freight'){
            List<Freight__c> serviceAux = [SELECT Id, Back_end_Coordinator__c, Back_end_Coordinator__r.Name FROM Freight__c WHERE Id = :vfpConfiguration.parentId];
            if(!serviceAux.isEmpty() && String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && serviceAux[0].Back_end_Coordinator__c != null) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__r.Name,null, 'User'));
        }else if(vfpConfiguration.parentSObject == 'Air'){
            List<Air__c> serviceAux = [SELECT Id, Back_end_Coordinator__c, Back_end_Coordinator__r.Name FROM Air__c WHERE Id = :vfpConfiguration.parentId];
            if(!serviceAux.isEmpty() && String.isBlank(associations.get(USER_GTBACKENDCOORDINATOR).associationId) && serviceAux[0].Back_end_Coordinator__c != null) associations.put(USER_GTBACKENDCOORDINATOR, new AssociationWrapper(serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__c, serviceAux[0].Back_end_Coordinator__r.Name,null, 'User'));
        }
        
        contactClientValue = associations.get(CONTACT_CLIENT).relativeId;
        vendorContacts = new Map<Id,Contact>();
        Map<String,Contact> contactMap = new Map<String,Contact>();
        if(bidSelected.Vendor__c != null){
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE AccountId =: bidSelected.Vendor__c]) contactMap.put(c.Id,c);
            if(bidSelected.Vendor__r.ParentId != null){
                for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE AccountId =: bidSelected.Vendor__r.ParentId]) contactMap.put(c.Id,c);
            }
        } else if(bidSelected.Provider__c != null){
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE AccountId =: bidSelected.Provider__c]) contactMap.put(c.Id,c);
            if(bidSelected.Provider__r.ParentId != null){
                for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE AccountId =: bidSelected.Provider__r.ParentId]) contactMap.put(c.Id,c);
            }
        }
        vendorContactOptions = new List<SelectOption>();
        vendorContactOptions.add(new SelectOption('','---None---'));
        for(Contact c : contactMap.values()){
            vendorContacts.put(c.Id,c);
            vendorContactOptions.add(new SelectOption(c.Id,c.Name));
        }
    }
    
    @RemoteAction
    global static String searchCity(String query){
        query = '%' + query + '%';
        List<wrapperData> cityList = new List<wrapperData>();
        for(City__c c : [SELECT Id, Name FROM City__c WHERE Name LIKE: query LIMIT 20]){
            cityList.add(new wrapperData(c.Id,c.Name,''));
        }
        return JSON.serialize(cityList);
    }
    
    @RemoteAction
    global static String searchAirport(String query){
        query = '%' + query + '%';
        List<wrapperData> airportList = new List<wrapperData>();
        String nameAux;
        for(Airport__c a : [SELECT Id, Name, Airport_Code__c, City__c, City__r.Name FROM Airport__c WHERE Name LIKE: query OR Airport_Code__c LIKE: query LIMIT 20]){
            nameAux = (a.Airport_Code__c != null ? a.Airport_Code__c + ' - ' : '') + a.Name + (a.City__c != null ? ' - ' + a.City__r.Name : '');
            airportList.add(new wrapperData(a.Id,nameAux,''));
        }
        return JSON.serialize(airportList);
    }
    
    @RemoteAction
    global static String searchAccount(String query, String recordtype){
        query = '%' + query + '%';
        List<wrapperData> accountList = new List<wrapperData>();
        for(Account a : [SELECT Id, Name FROM Account WHERE Name LIKE: query AND RecordType.Name =: recordtype LIMIT 20]){
            accountList.add(new wrapperData(a.Id,a.Name,''));
        }
        return JSON.serialize(accountList);
    }
    
    global class wrapperData{
        public String data;
        public String value;
        public String extra1;
        
        public wrapperData(String cdata, String cvalue, String cextra1){
            data = cdata;
            value = cvalue;
            extra1 = cextra1;
        }
    }
    
    public class AssociationWrapper {
        public String associationId {get;set;}
        public String relativeId {get;set;}
        public String name {get;set;}
        public String roles {get;set;}
        public String belongsTo {get;set;}
        
        public AssociationWrapper() {
            this.associationId = '';
            this.relativeId = '';
            this.name = '';
            this.roles = '';
            this.belongsTo = '';
        }
        
        public AssociationWrapper(String associationId, String relativeId, String name, String roles, String belongsTo) {
            this.associationId = associationId;
            this.relativeId = relativeId;
            this.name = name;
            this.roles = roles;
            this.belongsTo = belongsTo;
        }
    }
}```

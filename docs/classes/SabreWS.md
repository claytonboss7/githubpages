---
layout: default
title: SabreWS
parent: classes
---

```global class SabreWS {
    private static String userid = SabreWS__c.getOrgDefaults().User_ID__c; // 742083
    private static String passw = SabreWS__c.getOrgDefaults().Password__c;  //CL570284
    private static String ipcc = SabreWS__c.getOrgDefaults().IPCC__c; // 9RRJ
    private static String domain = SabreWS__c.getOrgDefaults().Domain__c; // AA
    private static String endpoint = SabreWS__c.getOrgDefaults().Endpoint__c; // https://sws-crt.cert.havail.sabre.com/
    private static String endpointRest = SabreWS__c.getOrgDefaults().Endpoint_Rest__c; // https://api-crt.cert.havail.sabre.com/
    
    public static HttpResponse getAccessToken(){
        Http http = new Http();
        HttpRequest req = new HttpRequest();
        req.setTimeout(120000);
        //V1:742083:9RRJ:AA
        String authorization = EncodingUtil.base64Encode(Blob.valueOf(EncodingUtil.base64Encode(Blob.valueOf('V1:'+userid+':'+ipcc+':AA')) + ':' + EncodingUtil.base64Encode(Blob.valueOf(passw))));
        req.setHeader('Authorization','Basic ' + authorization);
        req.setHeader('Content-Type','application/x-www-form-urlencoded');
        req.setHeader('grant_type','client_credentials');
        req.setEndpoint(endpointRest + 'v2/auth/token');
        req.setMethod('POST');
        HttpResponse response;
        if(!Test.isRunningTest()){
            response = http.send(req);
        }else{
            response = new HttpResponse();
            response.setStatusCode(200);
            response.setBody('{"access_token":"test"}');
        }
        system.debug(response.getBody());
        return response;
    }
    
    @future(callout=true)
    public static void getHotelRatingInfoRQByAccount(Set<Id> bidIds){
        HttpResponse responseToken = getAccessToken();
        if(responseToken.getStatusCode() == 200){
            String binaryToken = getBinaryToken();
           	Http http;
            HttpRequest req;
            HttpResponse response;
            JSONParser parser;
            Map<String, Object> root;
            Account accountRecord;
            Map<String,List<Account>> accountMap;
            Boolean findAccount;
            String sabreCode;
            String globalCode;
            String startDate;
            String endDate;
            Bid__c bidAux;
            List<Bid__c> bidList = new List<Bid__c>();
            List<Account> accountList = new List<Account>();
            for(Bid__c bid : [SELECT Id, Vendor__c, Vendor__r.Name, Vendor__r.City__r.City__c, Housing__c, Housing__r.Date_In__c, Housing__r.Date_Out__c FROM Bid__c WHERE Id IN: bidIds]){
                if(bid.Vendor__c != null && bid.Housing__c != null && bid.Housing__r.Date_In__c != null && bid.Housing__r.Date_Out__c != null){
                    accountMap = new Map<String,List<Account>>();
                    root = (Map<String, Object>) JSON.deserializeUntyped(responseToken.getBody());
                    http = new Http();
                    req = new HttpRequest();
                    req.setTimeout(120000);
                    req.setHeader('Authorization','Bearer ' + (String)root.get('access_token'));
                    req.setHeader('Accept','application/json');
                    req.setEndpoint(endpointRest + 'v1/hotels/utilities/autocomplete/hotelname?query='+ bid.Vendor__r.Name.replace(' ','%20') +'&limit=50');
                    req.setMethod('GET');
                    if(!Test.isRunningTest()){response = http.send(req);
                    }else{
                        response = new HttpResponse();
                        response.setStatusCode(200);
                        response.setBody('{"response":{"numFound":19,"start":0,"docs":[{"hotelCode":"100095440","sabreHotelCode":"49574","hotelName":"Andaz Liverpool Street London","latitude":"51.51771","longitude":"-0.08404","countryCode":"GB","countryName":"United Kingdom (the)","city":"LONDON"}]}}');
                    }
                    if(response.getStatusCode() == 200){
                        system.debug(response.getBody());
                        parser = JSON.createParser(response.getBody());
                        SabreAutocomplete sabreJson = (SabreAutocomplete)parser.readValueAs(SabreAutocomplete.class);
                        if(sabreJson != null && sabreJson.response.docs != null){
                            for(SabreAutocomplete.Docs doc : sabreJson.response.docs){
                                accountRecord = new Account(Name = doc.hotelName, Sabre_Hotel_Code__c = doc.sabreHotelCode, Global_Hotel_Code__c = doc.hotelCode, ShippingCountryCode = doc.countryCode, ShippingStateCode = doc.stateCode, ShippingCity = doc.city);
                                if(accountRecord.Name != null) accountMap.put(accountRecord.ShippingCity,accountMap.get(accountRecord.ShippingCity) != null ? (List<Account>)accountMap.get(accountRecord.ShippingCity).add(accountRecord) : new List<Account>{accountRecord});
                            }
                            
                            if(!accountMap.isEmpty()){
                                findAccount = false;
                                sabreCode = null;
                                globalCode = null;
                                for(String cityName : accountMap.keySet()){
                                    if(!findAccount){
                                        if(accountMap.get(cityName) != null){
                                            for(Account acc : accountMap.get(cityName)){
                                                if(cityName == bid.Vendor__r.City__r.City__c && acc.Name.toLowerCase().contains(bid.Vendor__r.Name.toLowerCase())){
                                                    sabreCode = acc.Sabre_Hotel_Code__c;
                                                    globalCode = acc.Global_Hotel_Code__c;
                                                    findAccount = true;
                                                    break;
                                                }
                                            }
                                        }
                                    }
                                }
                                system.debug('sabreCode: '+sabreCode);
                                system.debug('globalCode: '+globalCode);
                                if(sabreCode != null || globalCode != null){
                                    accountList.add(new Account(Id = bid.Vendor__c, Sabre_Hotel_Code__c = sabreCode, Global_Hotel_Code__c = globalCode));
                                    startDate = DateTime.newInstance(bid.Housing__r.Date_In__c.year(),bid.Housing__r.Date_In__c.month(),bid.Housing__r.Date_In__c.day()).format('YYY-MM-dd');
                                    endDate = Datetime.newInstance(bid.Housing__r.Date_Out__c.year(),bid.Housing__r.Date_Out__c.month(),bid.Housing__r.Date_Out__c.day()).format('YYY-MM-dd');
                                    response = getHotelRating(binaryToken, ipcc, sabreCode != null ? sabreCode : globalCode, sabreCode != null ? 'SABRE' : 'GLOBAL', startDate, endDate);
                                    system.debug(response.getStatusCode());
                                    if(response.getStatusCode() == 200){                                        
                                        bidAux = readResponseHotelRating(response.getBody());
                                        bidAux.Id = bid.Id;
                                        bidList.add(bidAux);
                                    }
                                }else{
                                    bidAux = new Bid__c(Id = bid.Id, Sabre_Response__c = 'Hotel not found in Sabre');
                                    bidList.add(bidAux);
                                }
                            }
                        }else{
                            bidAux = new Bid__c(Id = bid.Id, Sabre_Response__c = 'Hotel not found in Sabre');
                            bidList.add(bidAux);
                        }
                    }
                }
            }
            
            if(!accountList.isEmpty()){
                ApexUtil.AccountTrigger_Is_Enabled = false;
                update accountList;
                ApexUtil.AccountTrigger_Is_Enabled = true;
            }
            if(!bidList.isEmpty()){
                ApexUtil.BidTrigger_Is_Enabled = false;
                update bidList;
                ApexUtil.BidTrigger_Is_Enabled = true;
            }
        }
    }
    
    public static String getBinaryToken(){
        Http http = new Http();
        HttpRequest req = new HttpRequest();
        req.setTimeout(120000);
        req.setHeader('Content-Type','text/xml;charset=UTF-8');
        //req.setHeader('SOAPAction','EncodeDecodeLLSRQ');
        req.setEndpoint(endpoint);
        req.setMethod('POST');
        String body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sec="http://schemas.xmlsoap.org/ws/2002/12/secext" xmlns:mes="http://www.ebxml.org/namespaces/messageHeader" xmlns:ns="http://www.opentravel.org/OTA/2002/11">'+
                       '<soapenv:Header>'+
                          '<sec:Security>'+
                             '<sec:UsernameToken>'+
                                '<sec:Username>' + userid + '</sec:Username>'+
                                '<sec:Password>' + passw +'</sec:Password>'+
                                '<Organization>' + ipcc + '</Organization>'+
                                '<Domain>' + domain + '</Domain>'+
                             '</sec:UsernameToken>'+
                          '</sec:Security>'+
                          '<mes:MessageHeader>'+
                             '<mes:From>'+
                                '<mes:PartyId />'+
                             '</mes:From>'+
                             '<mes:To>'+
                                '<mes:PartyId />'+
                             '</mes:To>'+
                             '<mes:CPAId>' + ipcc + '</mes:CPAId>'+
                             '<mes:ConversationId>' + String.valueOf(DateTime.now().getTime() / 1000) + '</mes:ConversationId>'+
                             '<mes:Service>SessionCreateRQ</mes:Service>'+
                             '<mes:Action>SessionCreateRQ</mes:Action>'+
                          '</mes:MessageHeader>'+
                       '</soapenv:Header>'+
                       '<soapenv:Body>'+
                          '<ns:SessionCreateRQ>'+
                             '<ns:POS>'+
                                '<ns:Source PseudoCityCode="' + ipcc + '"/>'+
                             '</ns:POS>'+
                          '</ns:SessionCreateRQ>'+
                       '</soapenv:Body>'+
                    '</soapenv:Envelope>';
        req.setBody(body);
        HttpResponse response;
        if(!Test.isRunningTest()){
            response = http.send(req);
        }else{
            response = new HttpResponse();
            response.setStatusCode(200);
            response.setBody('<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">' +
                           '<soap-env:Header>' +
                              '<eb:MessageHeader eb:version="1.0" soap-env:mustUnderstand="1" xmlns:eb="http://www.ebxml.org/namespaces/messageHeader">' +
                                 '<eb:From>' +
                                    '<eb:PartyId eb:type="URI"/>' +
                                 '</eb:From>' +
                                 '<eb:To>' +
                                    '<eb:PartyId eb:type="URI"/>' +
                                 '</eb:To>' +
                                 '<eb:CPAId>9RRJ</eb:CPAId>' +
                                 '<eb:ConversationId>2</eb:ConversationId>' +
                                 '<eb:Service eb:type="sabreXML">Session</eb:Service>' +
                                 '<eb:Action>SessionCreateRS</eb:Action>' +
                                 '<eb:MessageData>' +
                                    '<eb:MessageId>2498967692607410151</eb:MessageId>' +
                                    '<eb:Timestamp>2020-04-23T19:14:20</eb:Timestamp>' +
                                 '</eb:MessageData>' +
                              '</eb:MessageHeader>' +
                              '<wsse:Security xmlns:wsse="http://schemas.xmlsoap.org/ws/2002/12/secext">' +
                                 '<wsse:BinarySecurityToken valueType="String" EncodingType="wsse:Base64Binary">code</wsse:BinarySecurityToken>' +
                              '</wsse:Security>' +
                           '</soap-env:Header>' +
                           '<soap-env:Body>' +
                              '<SessionCreateRS version="1" status="Approved" xmlns="http://www.opentravel.org/OTA/2002/11">' +
                                 '<ConversationId>2</ConversationId>' +
                              '</SessionCreateRS>' +
                           '</soap-env:Body>' +
                        '</soap-env:Envelope>');
        }
        String binaryToken;
        if(response.getStatusCode() == 200){
            List<Dom.XmlNode> dataToken = new List<Dom.XmlNode>();
            dataToken = XmlParser(response.getBody());
            for(Dom.XmlNode childElement1 : dataToken){
                for(Dom.XmlNode childElement2 : childElement1.getChildElements()){
                    if(childElement2.getName()=='Security'){
                        for(Dom.XmlNode childElement3 : childElement2.getChildElements()){
                            if(childElement3.getName()=='BinarySecurityToken'){
                                binaryToken = childElement3.getText();
                            }
                        }
                    }
                }
            }
        }
        system.debug(binaryToken);
        return binaryToken;
    }
    
    @AuraEnabled
    public static String getIATACode(Id cityId){
        String response = 'An error has occurred.';
        String binaryToken = SabreWs.getBinaryToken();
        City__c city = [SELECT Id, Name, City__c, Country__c, IATAN_Code__c, IATAN_Response__c, Start_Date__c, End_Date__c, Adults__c FROM City__c WHERE Id =: cityId];
        Map<String,String> responseMap;
        if(city.IATAN_Code__c == null){
            responseMap = getEncodeDecodeRQ(binaryToken,city.City__c);
        }else{
            responseMap = new Map<String,String>();
            responseMap.put('code',city.IATAN_Code__c);
            responseMap.put('text',city.IATAN_Response__c);
        }            
        if(responseMap != null){
            city.IATAN_Code__c = responseMap.get('code') != null ? responseMap.get('code') : '';
            city.IATAN_Response__c = responseMap.get('text') != null ? responseMap.get('text') : null;
            
            //GET HOTELS
            if(city.Start_Date__c != null && city.End_Date__c != null && city.Adults__c != null){
                Map<String,City__c> cityMap = new Map<String,City__c>();
                cityMap.put(city.Id,city);
                if(!cityMap.isEmpty()){
                    ApexUtil.CityTrigger_Is_Enabled = false;
                    Map<String,List<Object>> responseHotelMap = getHotelAvailRQ(cityMap);
                    
                    List<Account> accountList = (List<Account>)responseHotelMap.get('accounts');
                    List<City__c> cityList = (List<City__c>)responseHotelMap.get('cities');
                    if(!cityList.isEmpty()) update cityList;
                    if(!accountList.isEmpty()){
                        try{
                            upsertAccounts(accountList);
                            city.Sabre_Response__c = null;
                            update city;
                            response = 'Ok';
                        }catch(DMLException e ){
                            system.debug(e.getMessage());
                            response = 'Error : ' + e.getMessage();
                        }catch(Exception e){
                            system.debug(e.getMessage());
                            response = 'Error : ' + e.getMessage();
                        }
                    }else{
                        update city;
                        response = 'Ok';
                    }
                }
            }else{
                update city;
                response = 'Ok';
            }
            
        }
        return response;
    }
    
    public static void upsertAccounts(List<Account> accountList){
        if(!accountList.isEmpty()){
            Set<String> names = new Set<String>();
            for(Account a : accountList) names.add(a.Name);
            
            Map<String,Account> accountMap = new Map<String,Account>();
            String key;
            for(Account a : [SELECT Id, Name, City__c, City__r.Country__c, ShippingStreet, ShippingCity, ShippingStateCode, ShippingPostalCode, Phone, Amenity__c, Chain_Name__c, Sabre_Hotel_Code__c, Global_Hotel_Code__c FROM Account WHERE Name IN: names AND RecordTypeID =: Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Hotel_Vendor').getRecordTypeId()]){
                key = a.Name.toLowerCase() + (a.ShippingStreet != null ? a.ShippingStreet.toLowerCase() : '') + (a.ShippingCity != null ? a.ShippingCity.toLowerCase() : '') + (a.ShippingStateCode != null ? a.ShippingStateCode.toLowerCase() : '') + (a.ShippingPostalCode != null ? a.ShippingPostalCode.toLowerCase() : '');
                accountMap.put(key,a);
            }
            
            for(Account a : accountList){
                key = a.Name.toLowerCase() + (a.ShippingStreet != null ? a.ShippingStreet.toLowerCase() : '') + (a.ShippingCity != null ? a.ShippingCity.toLowerCase() : '') + (a.ShippingStateCode != null ? a.ShippingStateCode.toLowerCase() : '') + (a.ShippingPostalCode != null ? a.ShippingPostalCode.toLowerCase() : '');
                if(accountMap.get(key) != null){
                    a.Id = accountMap.get(key).Id;
                    a.Name = accountMap.get(key).Name;
                    if(accountMap.get(key).City__c != null) a.City__c = accountMap.get(key).City__c;
                    if(accountMap.get(key).ShippingStreet != null) a.ShippingStreet = accountMap.get(key).ShippingStreet;
                    if(accountMap.get(key).ShippingCity != null) a.ShippingCity = accountMap.get(key).ShippingCity;
                    if(accountMap.get(key).ShippingStateCode != null) a.ShippingStateCode = accountMap.get(key).ShippingStateCode;
                    if(accountMap.get(key).ShippingPostalCode != null) a.ShippingPostalCode = accountMap.get(key).ShippingPostalCode;
                    if(accountMap.get(key).Phone != null) a.Phone = accountMap.get(key).Phone;
                    if(accountMap.get(key).Amenity__c != null) a.Amenity__c = accountMap.get(key).Amenity__c;
                    if(accountMap.get(key).Chain_Name__c != null) a.Chain_Name__c = accountMap.get(key).Chain_Name__c;
                    if(accountMap.get(key).Sabre_Hotel_Code__c != null) a.Sabre_Hotel_Code__c = accountMap.get(key).Sabre_Hotel_Code__c;
                    if(accountMap.get(key).Global_Hotel_Code__c != null) a.Global_Hotel_Code__c = accountMap.get(key).Global_Hotel_Code__c;
                }
                a.RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Hotel_Vendor').getRecordTypeId();
            }
            
            upsert accountList;
        }
    }
    
    public static Map<String,String> getEncodeDecodeRQ(String binaryTokenInput,String cityName){
        Map<String,String> responseMap = new Map<String,String>();
        String binaryToken;
        if(binaryTokenInput == null || binaryTokenInput == '') binaryToken = getBinaryToken(); else binaryToken = binaryTokenInput;
        
        HttpResponse response;
        String IATANCode;
        String IATANCodeAllText = '';
        if(binaryToken != null && binaryToken != ''){
            Http http = new Http();
            HttpRequest req = new HttpRequest();
            req.setTimeout(120000);
            req.setHeader('Content-Type','text/xml;charset=UTF-8');
            //req.setHeader('SOAPAction','EncodeDecodeLLSRQ');
            req.setEndpoint(endpoint);
            req.setMethod('POST');
            String body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sec="http://schemas.xmlsoap.org/ws/2002/12/secext" xmlns:mes="http://www.ebxml.org/namespaces/messageHeader" xmlns:ns="http://webservices.sabre.com/sabreXML/2011/10">'+
                           '<soapenv:Header>'+
                              '<sec:Security>'+
                                 '<sec:BinarySecurityToken valueType="String" EncodingType="wsse:Base64Binary">' + binaryToken +'</sec:BinarySecurityToken>'+
                              '</sec:Security>'+
                              '<mes:MessageHeader>'+
                                 '<mes:From>'+
                                    '<mes:PartyId>app</mes:PartyId>'+
                                 '</mes:From>'+
                                 '<mes:To>'+
                                    '<mes:PartyId>webservices.sabre.com</mes:PartyId>'+
                                 '</mes:To>'+
                                 '<mes:CPAId>' + ipcc + '</mes:CPAId>'+
                                 '<mes:ConversationId>' + String.valueOf(DateTime.now().getTime() / 1000) + '</mes:ConversationId>'+
                                 '<mes:Service />'+
                                 '<mes:Action>EncodeDecodeLLSRQ</mes:Action>'+
                              '</mes:MessageHeader>'+
                           '</soapenv:Header>'+
                           '<soapenv:Body>'+
                              '<ns:EncodeDecodeRQ Version="2.0.0">'+
                                 '<ns:Encode>'+
                                    '<ns:Address>'+
                                       '<ns:CityName>' + cityName + '</ns:CityName>'+
                                    '</ns:Address>'+
                                 '</ns:Encode>'+
                              '</ns:EncodeDecodeRQ>'+
                           '</soapenv:Body>'+
                        '</soapenv:Envelope>';
            req.setBody(body);
            if(!Test.isRunningTest()){
                response = http.send(req);
            }else{
                response = new HttpResponse();
                response.setStatusCode(200);
                response.setBody('<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">' +
                               '<soap-env:Header>' +
                                  '<eb:MessageHeader eb:version="1.0" soap-env:mustUnderstand="1" xmlns:eb="http://www.ebxml.org/namespaces/messageHeader">' +
                                     '<eb:From>' +
                                        '<eb:PartyId eb:type="URI">webservices.sabre.com</eb:PartyId>' +
                                     '</eb:From>' +
                                     '<eb:To>' +
                                        '<eb:PartyId eb:type="URI">app</eb:PartyId>' +
                                     '</eb:To>' +
                                     '<eb:CPAId>9RRJ</eb:CPAId>' +
                                     '<eb:ConversationId>testcloudcreations</eb:ConversationId>' +
                                     '<eb:Service/>' +
                                     '<eb:Action>EncodeDecodeLLSRS</eb:Action>' +
                                     '<eb:MessageData>' +
                                        '<eb:MessageId>2510060698655320151</eb:MessageId>' +
                                        '<eb:Timestamp>2020-04-23T19:24:25</eb:Timestamp>' +
                                     '</eb:MessageData>' +
                                  '</eb:MessageHeader>' +
                                  '<wsse:Security xmlns:wsse="http://schemas.xmlsoap.org/ws/2002/12/secext">' +
                                     '<wsse:BinarySecurityToken valueType="String" EncodingType="wsse:Base64Binary">code</wsse:BinarySecurityToken>' +
                                  '</wsse:Security>' +
                               '</soap-env:Header>' +
                               '<soap-env:Body>' +
                                  '<EncodeDecodeRS Version="2.0.0" xmlns="http://webservices.sabre.com/sabreXML/2011/10" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:stl="http://services.sabre.com/STL/v01">' +
                                     '<stl:ApplicationResults status="Complete">' +
                                        '<stl:Success timeStamp="2020-04-23T14:24:25-05:00"/>' +
                                     '</stl:ApplicationResults>' +
                                     '<Text>LAX   LOS ANGELES, CALIFORNIA,USA</Text>' +
                                     '<Text>LSQ   LOS ANGELES    CL, CHILE</Text>' +
                                  '</EncodeDecodeRS>' +
                               '</soap-env:Body>' +
                            '</soap-env:Envelope>');
            }

            if(response.getStatusCode() == 200){
                List<Dom.XmlNode> dataToken = new List<Dom.XmlNode>();
                dataToken = XmlParser(response.getBody());
                for(Dom.XmlNode childElement1 : dataToken){
                    for(Dom.XmlNode childElement2 : childElement1.getChildElements()){
                        if(childElement2.getName()=='EncodeDecodeRS'){
                            for(Dom.XmlNode childElement3 : childElement2.getChildElements()){
                                if(childElement3.getName()=='Text'){
                                    system.debug(childElement3.getText());
                                    if(IATANCode == null) IATANCode = childElement3.getText() != null ? childElement3.getText().split(' ')[0] : null;
                                    IATANCodeAllText = IATANCodeAllText + (childElement3.getText() != null ? childElement3.getText() + '
 ' : '');
                                } 
                            }
                        }
                    }
                }
            }
            system.debug(IATANCode);
        }
        responseMap.put('code',IATANCode != null ? IATANCode : '');
        responseMap.put('text',IATANCodeAllText);
        
        return responseMap;
    }
    
    public static Map<String,List<Object>> getHotelAvailRQ(Map<String,City__c> cityMap){
        Map<String,List<Object>> responseMap = new Map<String,List<Object>>();
        List<Account> accountList = new List<Account>();
        List<City__c> cityList = new List<City__c>();
        String binaryToken = getBinaryToken();

        if(binaryToken != null && binaryToken != ''){
            Http http;
            HttpRequest req;
            String body;
            HttpResponse response;
            Set<String> names;
            
            Account acc;
            City__c ci;
            String amenities;
            String startDate;
            String endDate;
            Integer adults;
            for(City__c city : cityMap.values()){
                if(city.IATAN_Code__c != null && city.Start_Date__c != null && city.End_Date__c != null && city.Adults__c != null){
                    startDate = DateTime.newInstance(city.Start_Date__c.year(),city.Start_Date__c.month(),city.Start_Date__c.day()).format('YYY-MM-dd');
                    endDate = Datetime.newInstance(city.End_Date__c.year(),city.End_Date__c.month(),city.End_Date__c.day()).format('YYY-MM-dd');
                    adults = Integer.valueOf(city.Adults__c);
                    system.debug(startDate);
                    system.debug(endDate);
                    system.debug(adults);
                    http = new Http();
                    req = new HttpRequest();
                    req.setTimeout(120000);
                    req.setHeader('Content-Type','text/xml;charset=UTF-8');
                    req.setEndpoint(endpoint);
                    req.setMethod('POST');
                    body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sec="http://schemas.xmlsoap.org/ws/2002/12/secext" xmlns:mes="http://www.ebxml.org/namespaces/messageHeader" xmlns:v3="http://services.sabre.com/hotel/avail/v3_0_0">'+
                                   '<soapenv:Header>'+
                                      '<sec:Security>'+
                                         '<sec:BinarySecurityToken>' + binaryToken +'</sec:BinarySecurityToken>'+
                                      '</sec:Security>'+
                                      '<mes:MessageHeader>'+
                                         '<mes:From>'+
                                            '<mes:PartyId>app</mes:PartyId>'+
                                         '</mes:From>'+
                                         '<mes:To>'+
                                            '<mes:PartyId>webservices.sabre.com</mes:PartyId>'+
                                         '</mes:To>'+
                                         '<mes:CPAId>' + ipcc + '</mes:CPAId>'+
                                         '<mes:ConversationId>' + String.valueOf(DateTime.now().getTime() / 1000) + '</mes:ConversationId>'+
                                         '<mes:Service>GetHotelAvailRQ</mes:Service>'+
                                         '<mes:Action>GetHotelAvailRQ</mes:Action>'+
                                         '<mes:MessageData />'+
                                         '<mes:DuplicateElimination />'+
                                         '<mes:Description />'+
                                         '<mes:Action>GetHotelAvailRQ</mes:Action>'+
                                      '</mes:MessageHeader>'+
                                   '</soapenv:Header>'+
                                   '<soapenv:Body>'+
                                      '<v3:GetHotelAvailRQ version="3.0.0">'+
                                        '<v3:POS>'+
                                            '<v3:Source PseudoCityCode="'+ ipcc +'"/>'+
                                         '</v3:POS>'+
                                         '<v3:SearchCriteria>'+
                                            '<v3:GeoSearch>'+
                                               '<v3:GeoRef Radius="200" UOM="MI">'+
                                                  '<v3:RefPoint Value="'+ city.IATAN_Code__c +'" ValueContext="CODE" RefPointType="6"/>'+
                                               '</v3:GeoRef>'+
                                            '</v3:GeoSearch>'+
                                            '<v3:RateInfoRef CurrencyCode="USD" BestOnly="1">'+
                                                '<v3:StayDateRange StartDate="' + startDate + '" EndDate="' + endDate +'"/>'+
                                                '<v3:Rooms>'+
                                                    '<v3:Room Index="1" Adults="' + adults + '" />'+
                                                '</v3:Rooms>'+
                                                '<v3:InfoSource>100</v3:InfoSource>'+
                                            '</v3:RateInfoRef>'+
                                         '</v3:SearchCriteria>'+
                                      '</v3:GetHotelAvailRQ>'+
                                   '</soapenv:Body>'+
                                '</soapenv:Envelope>';
                    req.setBody(body);
                    if(!Test.isRunningTest()){
                        response = http.send(req);
                    }else{
                        response = new HttpResponse();
                        response.setStatusCode(200);
                        response.setBody('<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">' +
                                   '<soap-env:Header></soap-env:Header>' +
                                   '<soap-env:Body>' +
                                      '<ns25:GetHotelAvailRS xmlns:ns25="http://services.sabre.com/hotel/avail/v3_0_0" xmlns="http://services.sabre.com/STL_Payload/v02_01">' +
                                         '<ns25:HotelAvailInfos MaxSearchResults="1000" ShopKey="f7f78473-7161-4c89-aeab-408d6de60377" OffSet="1">' +
                                            '<ns25:HotelAvailInfo>' +
                                               '<ns25:HotelInfo HotelCode="100042216" SabreRating="3.0" BrandCode="10001" Direction="E" BrandName="Holiday Inn" UOM="MI" ChainName="Holiday Inn" ChainCode="HI" CodeContext="GLOBAL" Ordinal="1" SabreHotelCode="2282" HotelName="Holiday Inn International Arpt" Distance="2.13">' +
                                                  '<ns25:LocationInfo Latitude="33.946137" Longitude="-118.370059">' +
                                                     '<ns25:Address>' +
                                                        '<ns25:AddressLine1>9901 La Cienega Blvd</ns25:AddressLine1>' +
                                                        '<ns25:CityName CityCode="LAX">Los Angeles</ns25:CityName>' +
                                                        '<ns25:StateProv StateCode="CA"/>' +
                                                        '<ns25:PostalCode>90045</ns25:PostalCode>' +
                                                        '<ns25:CountryName Code="US">United States (the)</ns25:CountryName>' +
                                                     '</ns25:Address>' +
                                                     '<ns25:Contact Phone="310-649-5151" Fax="310-670-3619"/>' +
                                                  '</ns25:LocationInfo>' +
                                                  '<ns25:Amenities>' +
                                                     '<ns25:Amenity Description="Wheelchair access" Code="101"/>' +
                                                     '<ns25:Amenity Description="Family Room" Code="2014"/>' +
                                                  '</ns25:Amenities>' +
                                                  '<ns25:SecurityFeatures>' +
                                                     '<ns25:SecurityFeature Description="Complies with Local/State/Federal fire laws" Code="9">Y</ns25:SecurityFeature>' +
                                                  '</ns25:SecurityFeatures>' +
                                               '</ns25:HotelInfo>' +
                                               '<ns25:HotelRateInfo>' +
                                                  '<ns25:RateInfos>' +
                                                     '<ns25:RateInfo StartDate="2020-06-13" CurrencyCode="USD" AmountAfterTax="237.42" AmountBeforeTax="205.20" AverageNightlyRate="118.71" RateKey="LiMt2zo8iK" RateSource="100" EndDate="2020-06-15" TaxInclusive="true">' +
                                                        '<ns25:Commission Type="Percentage">' +
                                                           '<ns25:CommissionDescription>' +
                                                              '<ns25:Text>COMMISSIONABLE</ns25:Text>' +
                                                           '</ns25:CommissionDescription>' +
                                                        '</ns25:Commission>' +
                                                     '</ns25:RateInfo>' +
                                                  '</ns25:RateInfos>' +
                                               '</ns25:HotelRateInfo>' +
                                            '</ns25:HotelAvailInfo>' +
                                         '</ns25:HotelAvailInfos>' +
                                      '</ns25:GetHotelAvailRS>' +
                                   '</soap-env:Body>' +
                                '</soap-env:Envelope>');
                    }
        
                    names = new Set<String>();
                    system.debug(response.getStatusCode());
                    system.debug(response.getStatus());
                    system.debug(response.getBody());
                    if(response.getStatusCode() == 200){
                        List<Dom.XmlNode> dataToken = new List<Dom.XmlNode>();
                        dataToken = XmlParser(response.getBody());
                        for(Dom.XmlNode childElement1 : dataToken){
                            for(Dom.XmlNode childElement2 : childElement1.getChildElements()){
                                if(childElement2.getName()=='GetHotelAvailRS'){
                                    for(Dom.XmlNode childElement3 : childElement2.getChildElements()){
                                        if(childElement3.getName()=='ApplicationResults'){
                                             for(Dom.XmlNode childElement4 : childElement3.getChildElements()){
                                                 if(childElement4.getName()=='Warning'){
                                                     for(Dom.XmlNode childElement5 : childElement4.getChildElements()){
                                                         if(childElement5.getName()=='SystemSpecificResults'){
                                                             for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                                 if(childElement6.getName()=='Message'){
                                                                     ci = new City__c(Id = city.Id, Sabre_Response__c = childElement6.gettext());
                                                                     cityList.add(ci);
                                                                 }
                                                             }
                                                         }
                                                     }
                                                 }
                                             }
                                        }
                                        if(childElement3.getName()=='HotelAvailInfos'){
                                            for(Dom.XmlNode childElement4 : childElement3.getChildElements()){
                                                if(childElement4.getName()=='HotelAvailInfo'){
                                                    acc = new Account();
                                                    for(Dom.XmlNode childElement5 : childElement4.getChildElements()){
                                                        if(childElement5.getName()=='HotelInfo'){
                                                            acc.Name = childElement5.getAttribute('HotelName',null);
                                                            acc.City__c = city.Id;
                                                            acc.Chain_Name__c = childElement5.getAttribute('ChainName',null);
                                                            acc.Sabre_Hotel_Code__c = childElement5.getAttribute('SabreHotelCode',null);
                                                            acc.Global_Hotel_Code__c = childElement5.getAttribute('HotelCode',null);
                                                            acc.ShippingCountry = city.Country__c;
                                                            acc.BillingCountry = city.Country__c;
                                                            for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                                if(childElement6.getName()=='LocationInfo'){
                                                                    for(Dom.XmlNode childElement7 : childElement6.getChildElements()){
                                                                        if(childElement7.getName()=='Address'){
                                                                            for(Dom.XmlNode childElement8 : childElement7.getChildElements()){
                                                                                if(childElement8.getName()=='AddressLine1') acc.ShippingStreet = childElement8.getText();
                                                                                if(childElement8.getName()=='CityName') acc.ShippingCity = childElement8.getText();
                                                                                if(childElement8.getName()=='StateProv') acc.ShippingStateCode = childElement8.getAttribute('StateCode',null);
                                                                                if(childElement8.getName()=='PostalCode') acc.ShippingPostalCode = childElement8.getText();
                                                                            }
                                                                        }
                                                                        if(childElement7.getName()=='Contact') acc.Phone = childElement7.getAttribute('Phone',null);
                                                                    }
                                                                }
                                                                if(childElement6.getName()=='Amenities'){
                                                                    amenities = '';
                                                                    for(Dom.XmlNode childElement7 : childElement6.getChildElements()){
                                                                        if(childElement7.getName()=='Amenity') amenities = amenities + childElement7.getAttribute('Description',null) + ';';
                                                                    }
                                                                    acc.Amenity__c = amenities;
                                                                }
                                                            }
                                                        }
                                                    }
                                                    if(acc.Name != null && acc.Name.trim() != ''){
                                                        names.add(acc.Name);
                                                        accountList.add(acc);
                                                    }
                                                }
                                            }
                                        } 
                                    }
                                }
                            }
                        }
                    }
                }
			}
            
            system.debug(accountList);
        }
        
        responseMap.put('accounts',accountList);
        responseMap.put('cities',cityList);
        //return accountList;
        return responseMap;
    }
    
    public static HttpResponse getHotelRating(String binaryToken, String ipcc, String hotelCode, String hotelContext, String startDate, String endDate){
        HttpResponse response;
        Http http = new Http();
        HttpRequest req = new HttpRequest();
        req.setTimeout(120000);
        req.setHeader('Content-Type','text/xml;charset=UTF-8');
        req.setEndpoint(endpoint);
        req.setMethod('POST');
        String body = '<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:sec="http://schemas.xmlsoap.org/ws/2002/12/secext" xmlns:mes="http://www.ebxml.org/namespaces/messageHeader" xmlns:v3="http://services.sabre.com/hotel/rate/v3_0_0">' +
            '<soapenv:Header>' +
            '<sec:Security>' +
            '<sec:BinarySecurityToken>' + binaryToken + '</sec:BinarySecurityToken>' +
            '</sec:Security>' +
            '<mes:MessageHeader>' +
            '<mes:From>' +
            '<mes:PartyId>app</mes:PartyId>' +
            '</mes:From>' +
            '<mes:To>' +
            '<mes:PartyId>webservices.sabre.com</mes:PartyId>' +
            '</mes:To>' +
            '<mes:CPAId>' + ipcc + '</mes:CPAId>'+
            '<mes:ConversationId>' + String.valueOf(DateTime.now().getTime() / 1000) + '</mes:ConversationId>'+
            '<mes:Service>GetHotelRateInfoRQ</mes:Service>' +
            '<mes:Action>GetHotelRateInfoRQ</mes:Action>' +
            '<mes:MessageData />' +
            '<mes:DuplicateElimination />' +
            '<mes:Description />' +
            '</mes:MessageHeader>' +
            '</soapenv:Header>' +
            '<soapenv:Body>' +
            '<v3:GetHotelRateInfoRQ version="3.0.0">' +
            '<v3:POS>' +
            '<v3:Source PseudoCityCode="9RRJ"/>' +
            '</v3:POS>' +
            '<v3:HotelRefs>' +
            '<v3:HotelRef HotelCode="' + hotelCode + '" CodeContext="' + hotelContext +'"/>' +
            '</v3:HotelRefs>' +
            '<v3:RateInfoRef CurrencyCode="USD" PrepaidQualifier="IncludePrepaid" RefundableOnly="false">' +
            '<v3:StayDateRange StartDate="' + startDate + '" EndDate="' + endDate +'"/>' +
            '<v3:Rooms>' +
            '<v3:Room Index="1" Adults="1" />' +
            '</v3:Rooms>' +
            '</v3:RateInfoRef>' +
            '</v3:GetHotelRateInfoRQ>' +
            '</soapenv:Body>' +
            '</soapenv:Envelope>';
        req.setBody(body);
        if(!Test.isRunningTest()){
            response = http.send(req);
        }else{
            response = new HttpResponse();
            response.setStatusCode(200);
            response.setBody('<soap-env:Envelope xmlns:soap-env="http://schemas.xmlsoap.org/soap/envelope/">' +
                             '<soap-env:Header></soap-env:Header>' +
                             '<soap-env:Body>' +
                             '<ns20:GetHotelRateInfoRS xmlns:ns20="http://services.sabre.com/hotel/rate/v3_0_0">' +
                             '<ns20:ApplicationResults status="Complete">' +
                             '<ns20:Success timeStamp="2020-05-18T15:44:11.885-05:00"/>' +
                             '<ns20:Warning timeStamp="2020-05-18T15:44:11.873-05:00" type="Application">' +
                             '<ns20:SystemSpecificResults>' +
                             '<ns20:Message code="ERR.NGHP-AGGREGATOR.VAULT_API_ERROR">Exception occurred while Secret Vault API call for PCC {}9RRJ</ns20:Message>' +
                             '</ns20:SystemSpecificResults>' +
                             '</ns20:Warning>' +
                             '</ns20:ApplicationResults>' +
                             '<ns20:HotelRateInfos>' +
                             '<ns20:HotelRateInfo>' +
                             '<ns20:HotelInfo HotelCode="514" CodeContext="SABRE"/>' +
                             '<ns20:RateInfos>' +
                             '<ns20:RateInfo StartDate="2020-05-19" CurrencyCode="USD" AmountAfterTax="160.81" AdditionalFeesInclusive="true" AmountBeforeTax="139.00" AverageNightlyRate="160.81" RateKey="RoNgap" RateSource="100" EndDate="2020-05-20" TaxInclusive="true">' +
                             '<ns20:Commission Type="Variable">' +
                             '<ns20:CommissionDescription>' +
                             '<ns20:Text>COMMISSIONABLE</ns20:Text>' +
                             '</ns20:CommissionDescription>' +
                             '</ns20:Commission>' +
                             '</ns20:RateInfo>' +
                             '</ns20:RateInfos>' +
                             '</ns20:HotelRateInfo>' +
                             '</ns20:HotelRateInfos>' +
                             '</ns20:GetHotelRateInfoRS>' +
                             '</soap-env:Body>' +
                             '</soap-env:Envelope>');
        }
        return response;
    }
    
    public static Bid__c readResponseHotelRating(String dataResponse){
        Bid__c bid = new Bid__c();
        Decimal rate;
        List<Dom.XmlNode> dataToken = XmlParser(dataResponse);
        Integer cont;
        Integer contSelected;
        Integer cont2;
        for(Dom.XmlNode childElement1 : dataToken){
            for(Dom.XmlNode childElement2 : childElement1.getChildElements()){
                if(childElement2.getName()=='GetHotelRateInfoRS'){
                    for(Dom.XmlNode childElement3 : childElement2.getChildElements()){
                        if(childElement3.getName()=='HotelRateInfos'){
                            for(Dom.XmlNode childElement4 : childElement3.getChildElements()){
                                if(childElement4.getName()=='HotelRateInfo'){
                                    for(Dom.XmlNode childElement5 : childElement4.getChildElements()){
                                        if(childElement5.getName()=='RateInfos'){
                                            cont = 0;
                                            rate = null;
                                            for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                if(childElement6.getName()=='RateInfo'){
                                                    if(rate == null){
                                                        rate = Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null));
                                                        contSelected = cont;
                                                    }
                                                    else if(rate > Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null))){
                                                        rate = Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null));
                                                        contSelected = cont;
                                                    }
                                                    cont++;
                                                }
                                            }
                                            if(rate == null){
                                                cont = 0;
                                                for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                    if(childElement6.getName()=='ConvertedRateInfo'){
                                                        if(rate == null){
                                                            rate = Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null));
                                                            contSelected = cont;
                                                        }
                                                        else if(rate > Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null))){
                                                            rate = Decimal.valueOf(childElement6.getAttribute('AverageNightlyRate',null));
                                                            contSelected = cont;
                                                        }
                                                        cont++;
                                                    }
                                                }
                                            }
                                        }
                                        if(childElement5.getName()=='Rooms'){
                                            system.debug(contSelected);
                                            cont2 = 0;
                                            for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                if(childElement6.getName()=='Room'){
                                                    if(contSelected == cont2){
                                                        system.debug('Enter');
                                                        for(Dom.XmlNode childElement7 : childElement6.getChildElements()){
                                                            if(childElement7.getName()=='RoomDescription'){
                                                                for(Dom.XmlNode childElement8 : childElement7.getChildElements()){
                                                                    if(childElement8.getName()=='Text'){
                                                                        system.debug('enter2');
                                                                        bid.Room_Description__c = childElement8.getText();
                                                                    }
                                                                }
                                                            }
                                                            if(childElement7.getName()=='RatePlans'){
                                                                for(Dom.XmlNode childElement8 : childElement7.getChildElements()){
                                                                    if(childElement8.getName()=='RatePlan'){
                                                                        system.debug('enter3');
                                                                        bid.Rate_Plan_Name__c = childElement8.getAttribute('RatePlanName',null);
                                                                    }
                                                                }
                                                            }
                                                        }
                                                        break;
                                                    }
                                                    cont2++;
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                        if(rate == null){
                            if(childElement3.getName()=='ApplicationResults'){
                                for(Dom.XmlNode childElement4 : childElement3.getChildElements()){
                                    if(childElement4.getName()=='Error'){
                                        for(Dom.XmlNode childElement5 : childElement4.getChildElements()){
                                            if(childElement5.getName()=='SystemSpecificResults'){
                                                for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                    if(childElement6.getName()=='Message'){
                                                        bid.Sabre_Response__c = childElement6.getText();
                                                        system.debug(bid);
                                                        break;
                                                    }
                                                }
                                            }
                                        }
                                    }
                                    if(bid.Sabre_Response__c == null){
                                        if(childElement4.getName()=='Warning'){
                                            for(Dom.XmlNode childElement5 : childElement4.getChildElements()){
                                                if(childElement5.getName()=='SystemSpecificResults'){
                                                    for(Dom.XmlNode childElement6 : childElement5.getChildElements()){
                                                        if(childElement6.getName()=='Message'){
                                                            bid.Sabre_Response__c = childElement6.getText();
                                                            system.debug(bid);
                                                            break;
                                                        }
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
        if(rate != null){
            bid.Sabre_Rate__c  = String.valueOf(rate);
            bid.Sabre_Response__c = null;
        }
        return bid;
    }
    
    @future(callout=true)
    public static void getHotelRatingInfoRQ(Set<Id> bidIds){
        String binaryToken = getBinaryToken();

        if(binaryToken != null && binaryToken != ''){
            HttpResponse response;
            String startDate;
            String endDate;
            List<Bid__c> bidList = new List<Bid__c>();
            Bid__c bidAux;
            for(Bid__c bid : [SELECT Id, Vendor__c, Vendor__r.Sabre_Hotel_Code__c, Housing__c, Housing__r.Date_In__c, Housing__r.Date_Out__c FROM Bid__c WHERE Id IN: bidIds]){
                if(bid.Vendor__c != null && bid.Vendor__r.Sabre_Hotel_Code__c != null && bid.Housing__c != null && bid.Housing__r.Date_In__c != null && bid.Housing__r.Date_Out__c != null){
                    startDate = DateTime.newInstance(bid.Housing__r.Date_In__c.year(),bid.Housing__r.Date_In__c.month(),bid.Housing__r.Date_In__c.day()).format('YYY-MM-dd');
                    endDate = Datetime.newInstance(bid.Housing__r.Date_Out__c.year(),bid.Housing__r.Date_Out__c.month(),bid.Housing__r.Date_Out__c.day()).format('YYY-MM-dd');

                    response = getHotelRating(binaryToken, ipcc, bid.Vendor__r.Sabre_Hotel_Code__c, 'SABRE', startDate, endDate);
                    system.debug(response.getStatusCode());
                    if(response.getStatusCode() == 200){
                        bidAux = readResponseHotelRating(response.getBody());
                        bidAux.Id = bid.Id;
                        bidList.add(bidAux);
                    }
                }
            }
            
            if(!bidList.isEmpty()){
                ApexUtil.BidTrigger_Is_Enabled = false;
                update bidList;
                ApexUtil.BidTrigger_Is_Enabled = true;
            }
        }
    }
    
    public static List<Dom.XmlNode> XmlParser(String strXml) {
        List<Dom.XmlNode> childlist = new List<Dom.XmlNode>();
        Dom.Document doc = new Dom.Document();
        Integer childElementCount =0;
        doc.load(strXml);
        Dom.XMLNode rootElement = doc.getRootElement();
        String rootElementName = rootElement.getName();
        for(Dom.XmlNode childelement : rootElement.getChildElements()){
            childlist.add(childelement);
            childElementCount++;
        }
        return childlist;
    }
}```

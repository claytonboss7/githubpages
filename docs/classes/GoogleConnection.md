---
layout: default
title: GoogleConnection
parent: classes
---

```public class GoogleConnection {
    
	@future(callout=true)
	public static void ping(Set<Id> ids){
        GoogleMaps__c g = GoogleMaps__c.getOrgDefaults();
        Http http;
        HttpRequest req;
        HttpResponse response;
        List<Dom.XmlNode> distanceXML;
        List<City__c> cityList = new List<City__c>();
        String union;
        String latitude;
        String longitude;
        for(City__c c : [Select Id, City__c, State__c, Country__c From City__c WHERE Id IN: ids]){
            union = (c.City__c != null ? c.City__c.replace(' ','%20') + '+' : '') + (c.State__c != null ? c.State__c.replace(' ','%20') + '+' : '') + (c.Country__c != null ? c.Country__c.replace(' ','%20') : '');
            system.debug(union);
            latitude = '';
            longitude = '';
            
            http = new Http();
            req = new HttpRequest();
            req.setTimeout(120000);
            req.setEndpoint(g.Endpoint__c + 'geocode/xml?address=' + union + '&key=' + g.API_Key__c);
            req.setHeader('Accept','application/xml');
            req.setMethod('GET');       
            response = new HttpResponse();
            if(!Test.isRunningTest()){
                response = http.send(req);    
            }else{
                response.setStatusCode(200);
                response.setBody('<?xmlversion="1.0"encoding="UTF-8"?><GeocodeResponse><status>OK</status><result><type>locality</type><type>political</type><formatted_address>NewYork,NY,USA</formatted_address><address_component><long_name>NewYork</long_name><short_name>NewYork</short_name>'+
                                 '<type>locality</type><type>political</type></address_component><address_component><long_name>NewYork</long_name><short_name>NY</short_name><type>administrative_area_level_1</type><type>political</type></address_component><address_component>'+
                                 '<long_name>UnitedStates</long_name><short_name>US</short_name><type>country</type><type>political</type></address_component><geometry><location><lat>40.7127753</lat><lng>-74.0059728</lng></location><location_type>APPROXIMATE</location_type><viewport>'+
                                 '<southwest><lat>40.4773991</lat><lng>-74.2590899</lng></southwest><northeast><lat>40.9175771</lat><lng>-73.7002721</lng></northeast></viewport><bounds><southwest><lat>40.4773991</lat><lng>-74.2590899</lng></southwest><northeast><lat>40.9175771</lat>'+
                                 '<lng>-73.7002721</lng></northeast></bounds></geometry><place_id>ChIJOwg_06VPwokRYv534QaPC8g</place_id></result></GeocodeResponse>');
            }
            system.debug(response.getStatus());
            system.debug(response.getStatusCode());
            system.debug(response.getBody());
            c.Google_Response__c = response.getBody();
            if(response.getStatusCode() == 200){
                distanceXML = XmlParser(response.getBody());
                for(Dom.XmlNode childElement1 : distanceXML){
                    if(childElement1.getName()=='result'){
                        for(Dom.XmlNode childElement2:childElement1.getChildElements()){
                            if(childElement2.getName()=='geometry'){
                                for(Dom.XmlNode childElement3:childElement2.getChildElements()){
                                    if(childElement3.getName()=='location'){
                                        for(Dom.XmlNode childElement4:childElement3.getChildElements()){
                                            if(childElement4.getName()=='lat'){
                                                system.debug(childElement4.getText());
                                                latitude = childElement4.getText();
                                            }
                                            if(childElement4.getName()=='lng'){
                                                system.debug(childElement4.getText());
                                                longitude = childElement4.getText();
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
            if(latitude != '' && longitude != ''){
             	c.Formated_Address__c = c.City__c + (c.State__c != null ? ', ' + c.State__c : '') + (c.Country__c != null ? ', ' + c.Country__c : '');
                c.Name = c.Formated_Address__c;
                c.Google_Maps_URL__c = 'https://www.google.com/maps/@?api=1&map_action=map&center='+ latitude +',' + longitude+'&zoom=11';
            }            
            cityList.add(c);
        }
        ApexUtil.CityTrigger_Is_Enabled = false;
        if(cityList.size()>0) update cityList;
    }
    
    @future(callout=true)
	public static void verifyDistance(Set<Id> ids){
        GoogleMaps__c g = GoogleMaps__c.getOrgDefaults();
        Http http;
        HttpRequest req;
        HttpResponse response;
        List<Dom.XmlNode> distanceXML;
        List<Vendor_Venue__c> vendorVenueList = new List<Vendor_Venue__c>();
        String origin;
        String destination;
        for(Vendor_Venue__c vv : [SELECT Id, Distance_Type__c, Vendor__c, Vendor_Address__c, Vendor__r.ShippingStreet, Vendor__r.ShippingCity, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode, Vendor__r.ShippingCountry,
                                  Venue__c, Venue__r.ShippingStreet, Venue__r.ShippingCity, Venue__r.ShippingState, Venue__r.ShippingPostalCode, Venue__r.ShippingCountry FROM Vendor_Venue__c WHERE Id IN: ids]){
            if(vv.Vendor__c != null && vv.Venue__c != null){
                origin = (vv.Vendor__r.ShippingStreet != null ? vv.Vendor__r.ShippingStreet.replace(' ','%20') + '+' : '') + 
                    		(vv.Vendor__r.ShippingCity != null ? vv.Vendor__r.ShippingCity.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingState != null ? vv.Vendor__r.ShippingState.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingPostalCode != null ? vv.Vendor__r.ShippingPostalCode.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingCountry != null ? vv.Vendor__r.ShippingCountry.replace(' ','%20') : '');
                destination = (vv.Venue__r.ShippingStreet != null ? vv.Venue__r.ShippingStreet.replace(' ','%20') + '+' : '') + 
                    		(vv.Venue__r.ShippingCity != null ? vv.Venue__r.ShippingCity.replace(' ','%20') + '+' : '') +
                            (vv.Venue__r.ShippingState != null ? vv.Venue__r.ShippingState.replace(' ','%20') + '+' : '') +
                            (vv.Venue__r.ShippingPostalCode != null ? vv.Venue__r.ShippingPostalCode.replace(' ','%20') + '+' : '') +
                            (vv.Venue__r.ShippingCountry != null ? vv.Venue__r.ShippingCountry.replace(' ','%20') : '');
                
                http = new Http();
                req = new HttpRequest();
                req.setTimeout(120000);
                req.setEndpoint(g.Endpoint__c + 'distancematrix/xml?units=imperial&origins='+origin+'&destinations=' + destination + '&key=' + g.API_Key__c);
                system.debug(req.getEndpoint());
                req.setMethod('GET');       
                response = new HttpResponse();
                if(!Test.isRunningTest()){
                	response = http.send(req);    
                }else{
                    response.setStatusCode(200);
                    response.setBody('<DistanceMatrixResponse><status>OK</status><origin_address>Anaheim,California,EE.UU.</origin_address><destination_address>Pasadena,California,EE.UU.</destination_address><row><element><status>OK</status><duration><value>2884</value><text>48min</text></duration><distance><value>70138</value><text>43.6 mi</text></distance></element></row></DistanceMatrixResponse>');
                }

                system.debug(response.getStatusCode());
                system.debug(response.getStatus());
                system.debug(response.getBody());
                if(response.getStatusCode() == 200){
                    distanceXML = XmlParser(response.getBody());
                    for(Dom.XmlNode childElement1 : distanceXML){
                        if(childElement1.getName()=='row'){
                            for(Dom.XmlNode childElement2:childElement1.getChildElements()){
                                if(childElement2.getName()=='element'){
                                    for(Dom.XmlNode childElement3:childElement2.getChildElements()){
                                        if(childElement3.getName()=='distance'){
                                            for(Dom.XmlNode childElement4:childElement3.getChildElements()){
                                                if(childElement4.getName()=='value'){
                                                    system.debug(childElement4.getText());
                                                    if(vv.Distance_Type__c == 'Mile(s)'){
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText())/1609.34; // 1 Mile = 1609.34 Metre
                                                    }
                                                    else if(vv.Distance_Type__c == 'Km(s)'){
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText())/1000; // 1 KM = 1000 Metre
                                                        vv.Distance_Type__c = 'Km(s)';
                                                    }else{
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText());
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                    vendorVenueList.add(vv);
                }
            }
        }
        
        ApexUtil.VendorVenueTrigger_Is_Enabled = false;
        if(vendorVenueList.size()>0) update vendorVenueList;
    }
    
    @future(callout=true)
	public static void verifyDistanceAirport(Set<Id> ids){
        GoogleMaps__c g = GoogleMaps__c.getOrgDefaults();
        Http http;
        HttpRequest req;
        HttpResponse response;
        List<Dom.XmlNode> distanceXML;
        List<Vendor_Airport_Association__c> vendorAirportList = new List<Vendor_Airport_Association__c>();
        String origin;
        String destination;
        for(Vendor_Airport_Association__c vv : [SELECT Id, Distance_Type__c, Vendor__c, Vendor__r.ShippingStreet, Vendor__r.ShippingCity, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode, Vendor__r.ShippingCountry,
                                  Airport__c, Airport__r.City__c, Airport__r.Street_Address__c, Airport__r.City__r.City__c, Airport__r.City__r.State__c, Airport__r.Zipcode__c, Airport__r.City__r.Country__c 
                                                FROM Vendor_Airport_Association__c WHERE Id IN: ids]){
            if(vv.Vendor__c != null && vv.Airport__c != null){
                origin = (vv.Vendor__r.ShippingStreet != null ? vv.Vendor__r.ShippingStreet.replace(' ','%20') + '+' : '') + 
                    		(vv.Vendor__r.ShippingCity != null ? vv.Vendor__r.ShippingCity.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingState != null ? vv.Vendor__r.ShippingState.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingPostalCode != null ? vv.Vendor__r.ShippingPostalCode.replace(' ','%20') + '+' : '') +
                            (vv.Vendor__r.ShippingCountry != null ? vv.Vendor__r.ShippingCountry.replace(' ','%20') : '');
                destination = (vv.Airport__r.Street_Address__c != null ? vv.Airport__r.Street_Address__c.replace(' ','%20') + '+' : '') + 
                    		(vv.Airport__r.City__r.City__c != null ? vv.Airport__r.City__r.City__c.replace(' ','%20') + '+' : '') +
                            (vv.Airport__r.City__r.State__c != null ? vv.Airport__r.City__r.State__c.replace(' ','%20') + '+' : '') +
                            (vv.Airport__r.Zipcode__c != null ? vv.Airport__r.Zipcode__c.replace(' ','%20') + '+' : '') +
                            (vv.Airport__r.City__r.Country__c != null ? vv.Airport__r.City__r.Country__c.replace(' ','%20') : '');
                
                http = new Http();
                req = new HttpRequest();
                req.setTimeout(120000);
                req.setEndpoint(g.Endpoint__c + 'distancematrix/xml?units=imperial&origins='+origin+'&destinations=' + destination + '&key=' + g.API_Key__c);
                system.debug(req.getEndpoint());
                req.setMethod('GET');       
                response = new HttpResponse();
                if(!Test.isRunningTest()){
                	response = http.send(req);    
                }else{
                    response.setStatusCode(200);
                    response.setBody('<DistanceMatrixResponse><status>OK</status><origin_address>Anaheim,California,EE.UU.</origin_address><destination_address>Pasadena,California,EE.UU.</destination_address><row><element><status>OK</status><duration><value>2884</value><text>48min</text></duration><distance><value>70138</value><text>43.6 mi</text></distance></element></row></DistanceMatrixResponse>');
                }

                system.debug(response.getStatusCode());
                system.debug(response.getStatus());
                system.debug(response.getBody());
                if(response.getStatusCode() == 200){
                    distanceXML = XmlParser(response.getBody());
                    for(Dom.XmlNode childElement1 : distanceXML){
                        if(childElement1.getName()=='row'){
                            for(Dom.XmlNode childElement2:childElement1.getChildElements()){
                                if(childElement2.getName()=='element'){
                                    for(Dom.XmlNode childElement3:childElement2.getChildElements()){
                                        if(childElement3.getName()=='distance'){
                                            for(Dom.XmlNode childElement4:childElement3.getChildElements()){
                                                if(childElement4.getName()=='value'){
                                                    system.debug(childElement4.getText());
                                                    if(vv.Distance_Type__c == 'Mile(s)'){
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText())/1609.34; // 1 Mile = 1609.34 Metre
                                                    }
                                                    else if(vv.Distance_Type__c == 'Km(s)'){
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText())/1000; // 1 KM = 1000 Metre
                                                        vv.Distance_Type__c = 'Km(s)';
                                                    }else{
                                                        vv.Distance__c = Decimal.valueOf(childElement4.getText());
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                    vendorAirportList.add(vv);
                }
            }
        }
        
        ApexUtil.VendorAirportTrigger_Is_Enabled = false;
        if(vendorAirportList.size()>0) update vendorAirportList;
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

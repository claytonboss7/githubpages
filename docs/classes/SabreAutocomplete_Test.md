---
layout: default
title: SabreAutocomplete_Test
parent: classes
---

```@IsTest
public class SabreAutocomplete_Test {
	
	// This test method should give 100% coverage
	static testMethod void testParse() {
		String json = '{'+
		'  \"responseHeader\":{'+
		'    \"status\":0,'+
		'    \"QTime\":11},'+
		'  \"response\":{\"numFound\":7722,\"start\":0,\"docs\":['+
		'      {'+
		'        \"hotelCode\":\"100111742\",'+
		'        \"sabreHotelCode\":\"58304\",'+
		'        \"hotelName\":\"Hilton Garden Inn Hilton Head\",'+
		'        \"latitude\":\"32.235039\",'+
		'        \"longitude\":\"-80.80404\",'+
		'        \"countryCode\":\"US\",'+
		'        \"countryName\":\"United States (the)\",'+
		'        \"city\":\"Hilton Head Island\",'+
		'        \"stateCode\":\"SC\"}'+
		']'+
		'  }}';
		SabreAutocomplete r = SabreAutocomplete.parse(json);
		System.assert(r != null);

		json = '{\"TestAMissingObject\": { \"TestAMissingArray\": [ { \"TestAMissingProperty\": \"Some Value\" } ] } }';
		SabreAutocomplete.Response objResponse = new SabreAutocomplete.Response(System.JSON.createParser(json));
		System.assert(objResponse != null);
		System.assert(objResponse.numFound == null);
		System.assert(objResponse.start == null);
		System.assert(objResponse.docs == null);

		json = '{\"TestAMissingObject\": { \"TestAMissingArray\": [ { \"TestAMissingProperty\": \"Some Value\" } ] } }';
		SabreAutocomplete.ResponseHeader objResponseHeader = new SabreAutocomplete.ResponseHeader(System.JSON.createParser(json));
		System.assert(objResponseHeader != null);
		System.assert(objResponseHeader.status == null);
		System.assert(objResponseHeader.QTime == null);

		json = '{\"TestAMissingObject\": { \"TestAMissingArray\": [ { \"TestAMissingProperty\": \"Some Value\" } ] } }';
		SabreAutocomplete obj = new SabreAutocomplete(System.JSON.createParser(json));
		System.assert(obj != null);
		System.assert(obj.responseHeader == null);
		System.assert(obj.response == null);

		json = '{\"TestAMissingObject\": { \"TestAMissingArray\": [ { \"TestAMissingProperty\": \"Some Value\" } ] } }';
		SabreAutocomplete.Docs objDocs = new SabreAutocomplete.Docs(System.JSON.createParser(json));
		System.assert(objDocs != null);
		System.assert(objDocs.hotelCode == null);
		System.assert(objDocs.sabreHotelCode == null);
		System.assert(objDocs.hotelName == null);
		System.assert(objDocs.latitude == null);
		System.assert(objDocs.longitude == null);
		System.assert(objDocs.countryCode == null);
		System.assert(objDocs.countryName == null);
		System.assert(objDocs.city == null);
		System.assert(objDocs.stateCode == null);
	}
}```

---
layout: default
title: rcsfl__AdminCenterHelper
parent: pages
---

```<apex:page sidebar="false" showHeader="false">

<script>
    var message = {
        type: 'adminCenterHelperInitialized'
    };
    parent.postMessage(message, '*');

    window.addEventListener('message', function(event) {
        if (event.data) {
            if (event.data.type === 'createCallCenter') {
                createCallCenter(event.data.name, event.data.adapterUrl);
            } else if (event.data.type === 'getLayouts') {
                getLayouts();
            } else if (event.data.type === 'toggleLayoutField') {
                toggleLayoutField(event.data.layoutName, event.data.fieldName, event.data.addField);
            }
        }
    });

    let request = obj => {
        return new Promise((resolve, reject) => {
            let xhr = new XMLHttpRequest();
            xhr.open(obj.method || 'GET', obj.url);
            if (obj.headers) {
                Object.keys(obj.headers).forEach(key => {
                    xhr.setRequestHeader(key, obj.headers[key]);
                });
            }
            xhr.onload = () => {
                if (xhr.status >= 200 && xhr.status < 300) {
                    resolve({
                        statusCode: xhr.status,
                        statusText: xhr.statusText,
                        body: xhr.response
                    });
                } else {
                    reject({
                        statusCode: xhr.status,
                        statusText: xhr.statusText,
                        body: xhr.response
                    });
                }
            };
            xhr.onerror = () => {
                reject({
                    statusCode: xhr.status,
                    statusText: xhr.statusText,
                    body: xhr.response
                });
            };
            xhr.send(obj.body);
        });
    };

    function createCallCenter(name, adapterUrl) {
        var body = '<?xml version="1.0" encoding="utf-8"?>'
                 + '<env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">'
                 +   '<env:Header>'
                 +     '<urn:SessionHeader xmlns:urn="http://soap.sforce.com/2006/04/metadata">'
                 +       '<urn:sessionId>{!$Api.Session_Id}</urn:sessionId>'
                 +     '</urn:SessionHeader>'
                 +   '</env:Header>'
                 +   '<env:Body>'
                 +     '<createMetadata xmlns="http://soap.sforce.com/2006/04/metadata">'
                 +       '<metadata xsi:type="CallCenter">'
                 +         '<fullName>RingCentral</fullName>'
                 +         '<displayName>' + name + '</displayName>'
                 +         '<adapterUrl>' + adapterUrl + '</adapterUrl>'
                 +         '<customSettings>{&quot;reqSoftphoneHeight&quot;:&quot;450&quot;,&quot;reqUseApi&quot;:&quot;true&quot;,&quot;reqSoftphoneWidth&quot;:&quot;300&quot;,&quot;reqSalesforceCompatibilityMode&quot;:&quot;Classic_and_Lightning&quot;}</customSettings>'
                 +         '<displayNameLabel>Display Name</displayNameLabel>'
                 +         '<internalNameLabel>InternalName</internalNameLabel>'
                 +         '<sections>'
                 +           '<items>'
                 +             '<label>CTI Adapter URL</label>'
                 +             '<name>reqAdapterUrl</name>'
                 +             '<value>' + adapterUrl + '</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>Use CTI API</label>'
                 +             '<name>reqUseApi</name>'
                 +             '<value>true</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>Softphone Height</label>'
                 +             '<name>reqSoftphoneHeight</name>'
                 +             '<value>450</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>Softphone Width</label>'
                 +             '<name>reqSoftphoneWidth</name>'
                 +             '<value>300</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>Salesforce Compatibility Mode</label>'
                 +             '<name>reqSalesforceCompatibilityMode</name>'
                 +             '<value>Classic_and_Lightning</value>'
                 +           '</items>'
                 +           '<label>General Information</label>'
                 +           '<name>reqGeneralInfo</name>'
                 +         '</sections>'
                 +         '<sections>'
                 +           '<items>'
                 +             '<label>Outside Prefix</label>'
                 +             '<name>reqOutsidePrefix</name>'
                 +             '<value>9</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>Long Distance Prefix</label>'
                 +             '<name>reqLongDistPrefix</name>'
                 +             '<value>1</value>'
                 +           '</items>'
                 +           '<items>'
                 +             '<label>International Prefix</label>'
                 +             '<name>reqInternationalPrefix</name>'
                 +             '<value>01</value>'
                 +           '</items>'
                 +           '<label>Dialing Options</label>'
                 +           '<name>reqDialingOptions</name>'
                 +         '</sections>'
                 +       '</metadata>'
                 +     '</createMetadata>'
                 +   '</env:Body>'
                 + '</env:Envelope>';

        request({
            method: 'POST',
            url: '/services/Soap/m/48.0',
            headers: {
                'SOAPAction': '""',
                'Content-Type': 'text/xml'
            },
            body: body
        }).then(response => {
            var doc = new DOMParser().parseFromString(response.body, 'application/xml');
            var successElements = doc.getElementsByTagName('success');
            var success = false;

            if (successElements.length == 1 && successElements[0].childNodes[0].nodeValue == 'true') {
                success = true;
            }

            var message = {
                type: 'callCenterCreated',
                success: success
            };
            parent.postMessage(message, '*');
        }).catch(response => {
            var message = {
                type: 'callCenterCreated',
                created: false
            };
            parent.postMessage(message, '*');
        });
    }

    function getLayouts() {
        var body = '<?xml version="1.0" encoding="utf-8"?>'
                 + '<env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">'
                 +   '<env:Header>'
                 +     '<urn:SessionHeader xmlns:urn="http://soap.sforce.com/2006/04/metadata">'
                 +       '<urn:sessionId>{!$Api.Session_Id}</urn:sessionId>'
                 +     '</urn:SessionHeader>'
                 +   '</env:Header>'
                 +   '<env:Body>'
                 +     '<listMetadata xmlns="http://soap.sforce.com/2006/04/metadata">'
                 +       '<queries>'
                 +         '<type>Layout</type>'
                 +       '</queries>'
                 +     '</listMetadata>'
                 +   '</env:Body>'
                 + '</env:Envelope>';

        request({
            method: 'POST',
            url: '/services/Soap/m/48.0',
            headers: {
                'SOAPAction': '""',
                'Content-Type': 'text/xml'
            },
            body: body
        }).then(response => {
            var doc = new DOMParser().parseFromString(response.body, 'application/xml');
            var resultElements = doc.getElementsByTagName('result');

            var layouts = [];

            for (var i = 0; i < resultElements.length; i++) {
                var fullNameElements = resultElements[i].getElementsByTagName('fullName');
                var namespacePrefixElements = resultElements[i].getElementsByTagName('namespacePrefix');

                var layout = {
                    name: fullNameElements[0].childNodes[0].nodeValue
                };

                if (namespacePrefixElements.length > 0) {
                    layout.namespace = namespacePrefixElements[0].childNodes[0].nodeValue;
                }

                layouts.push(layout);
            }

            var message = {
                type: 'layouts',
                layouts: layouts
            };
            parent.postMessage(message, '*');
        }).catch(response => {
        });
    }

    function toggleLayoutField(layoutName, fieldName, addField) {
        var body = '<?xml version="1.0" encoding="utf-8"?>'
                 + '<env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">'
                 +   '<env:Header>'
                 +     '<urn:SessionHeader xmlns:urn="http://soap.sforce.com/2006/04/metadata">'
                 +       '<urn:sessionId>{!$Api.Session_Id}</urn:sessionId>'
                 +     '</urn:SessionHeader>'
                 +   '</env:Header>'
                 +   '<env:Body>'
                 +     '<readMetadata xmlns="http://soap.sforce.com/2006/04/metadata">'
                 +       '<type>Layout</type>'
                 +       '<type>' + layoutName + '</type>'
                 +     '</readMetadata>'
                 +   '</env:Body>'
                 + '</env:Envelope>';

        request({
            method: 'POST',
            url: '/services/Soap/m/48.0',
            headers: {
                'SOAPAction': '""',
                'Content-Type': 'text/xml'
            },
            body: body
        }).then(response => {
            var doc = new DOMParser().parseFromString(response.body, 'application/xml');
            var fieldElements = doc.getElementsByTagName('field');

            var layoutHasField = false;
            var fieldElement;

            for (var i = 0; i < fieldElements.length; i++) {
                if (fieldName == fieldElements[i].childNodes[0].nodeValue) {
                    layoutHasField = true;
                    fieldElement = fieldElements[i];
                    break;
                }
            }

            if (addField != layoutHasField) {
                // Add field to layout.
                if (addField && !layoutHasField) {
                    var behaviorElement = doc.createElement('behavior');
                    behaviorElement.appendChild(doc.createTextNode('Readonly'));

                    var fieldElement = doc.createElement('field');
                    fieldElement.appendChild(doc.createTextNode(fieldName));

                    var layoutItemsElement = doc.createElement('layoutItems');
                    layoutItemsElement.appendChild(behaviorElement);
                    layoutItemsElement.appendChild(fieldElement);

                    var layoutColumnsElements = doc.getElementsByTagName('layoutColumns');
                    layoutColumnsElements[0].appendChild(layoutItemsElement);
                }

                // Remove field from layout.
                else if (!addField && layoutHasField) {
                    fieldElement.parentNode.parentNode.removeChild(fieldElement.parentNode);
                }

                var recordXml = new XMLSerializer().serializeToString(doc.getElementsByTagName('records')[0]);
                recordXml = recordXml.replace(/<records.+?>/g, '').replace('</records>', '');

                var body = '<?xml version="1.0" encoding="utf-8"?>'
                         + '<env:Envelope xmlns:env="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">'
                         +   '<env:Header>'
                         +     '<urn:SessionHeader xmlns:urn="http://soap.sforce.com/2006/04/metadata">'
                         +       '<urn:sessionId>{!$Api.Session_Id}</urn:sessionId>'
                         +     '</urn:SessionHeader>'
                         +   '</env:Header>'
                         +   '<env:Body>'
                         +     '<updateMetadata xmlns="http://soap.sforce.com/2006/04/metadata">'
                         +       '<metadata xsi:type="Layout">'
                         +         recordXml
                         +       '</metadata>'
                         +     '</updateMetadata>'
                         +   '</env:Body>'
                         + '</env:Envelope>';

                request({
                    method: 'POST',
                    url: '/services/Soap/m/48.0',
                    headers: {
                        'SOAPAction': '""',
                        'Content-Type': 'text/xml'
                    },
                    body: body
                }).then(response => {
                    var doc = new DOMParser().parseFromString(response.body, 'application/xml');
                    var successElements = doc.getElementsByTagName('success');
                    var success = false;

                    if (successElements.length == 1 && successElements[0].childNodes[0].nodeValue == 'true') {
                        success = true;
                    }

                    var message = {
                        type: 'layoutFieldToggled',
                        layoutName: layoutName,
                        addField: addField,
                        success: success
                    };
                    parent.postMessage(message, '*');
                }).catch(response => {
                    var message = {
                        type: 'layoutFieldToggled',
                        layoutName: layoutName,
                        addField: addField,
                        success: false
                    };
                    parent.postMessage(message, '*');
                });
            }
        }).catch(response => {
            var message = {
                type: 'layoutFieldToggled',
                layoutName: layoutName,
                addField: addField,
                success: false
            };
            parent.postMessage(message, '*');
        });
    }
</script>

</apex:page>```

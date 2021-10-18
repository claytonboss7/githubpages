---
layout: default
title: AVSFQB__InvoiceDisplay
parent: scontrols
---

```<html> 
<head> 
<link href="/dCSS/Theme2/default/common.css" type="text/css" media="handheld,print,projection,screen,tty,tv" rel="stylesheet" > 
<link href="/dCSS/Theme2/default/custom.css" type="text/css" media="handheld,print,projection,screen,tty,tv" rel="stylesheet" > 

<script type="text/javascript" src="/js/functions.js"></script> 
<script src="/soap/ajax/8.0/connection.js"></script> 
</head> 
<script language="javascript"> 


function createTable(){ 
//document.getElementById('company').innerHTML = '<b>Job:</b> invxml.XMLDocument.selectSingleNode("root/CustomerRef/FullName").text; 
s = '<b>Invoice Date:</b>'+invxml.XMLDocument.selectSingleNode("root/TxnDate").text; 
s+='<br/><b>Invoice No:</b>'+invxml.XMLDocument.selectSingleNode("root/RefNumber").text; 

document.getElementById('txndate').innerHTML =s; 

document.getElementById('billto').innerHTML = invxml.XMLDocument.selectSingleNode("root/BillAddress/Addr1").text +'<br/>'; 

try { 
document.getElementById('billto').innerHTML += invxml.XMLDocument.selectSingleNode("root/BillAddress/City").text +'<br/>'; 
} catch (error){} 

try { 

document.getElementById('billto').innerHTML += invxml.XMLDocument.selectSingleNode("root/BillAddress/State").text +','; 
} catch (error){} 

try { 
document.getElementById('billto').innerHTML += invxml.XMLDocument.selectSingleNode("root/BillAddress/PostalCode").text +'<br/>'; 
} catch (error){} 


var productNodes = invxml.XMLDocument.selectNodes('root/DataExtRet'); 

if (productNodes.length>0){ 

s='<table width=70% border=0 bgcolor=#cccccc><tr>'; 
for (i=0;i<productNodes.length;i++) 
{ 
productNode = productNodes[i].selectSingleNode("DataExtName").text; 
s += '<td bgcolor=#cccccc>'+productNode +'</td>'; 
} 
s+='</tr><tr>'; 
for (i=0;i<productNodes.length;i++) 
{ 

s += '<td bgcolor=#ffffff>'+productNodes[i].selectSingleNode("DataExtValue").text+'</td>'; 
} 
s+='</tr></table>'; 

document.getElementById('dataext').innerHTML=s; 
} 

productNodes = invxml.XMLDocument.selectNodes('root/InvoiceLineRet'); 

s='<table border=0 width=100% bgcolor=#cccccc>'; 
s += '<tr>'; 
s += '<td width=20% bgcolor=#cccccc><b>Name</b></td>'; 
s += '<td width=30% bgcolor=#cccccc><b>Description</b></td>'; 
s += '<td width=10% bgcolor=#cccccc><b>Quantity</b></td>'; 
s += '<td width=20% bgcolor=#cccccc><b>Rate</b></td>'; 
s += '<td width=20% bgcolor=#cccccc><b>Amount</b></td>'; 
s += '</tr>'; 

for (i=0;i<productNodes.length;i++) 
{ 
s += '<tr>'; 

try{ 
s += '<td width=20% bgcolor=#ffffff>'+productNodes[i].selectSingleNode("ItemRef/FullName").text+'</td>'; 
} catch (error){ 
s += '<td width=20% bgcolor=#ffffff>&nbsp;</td>'; 
} 
try{ 
s += '<td width=30% bgcolor=#ffffff>'+productNodes[i].selectSingleNode("Desc").text+'</td>'; 
} catch (error) { 
s += '<td width=20% bgcolor=#ffffff>&nbsp;</td>'; 
} 

try { 
s += '<td width=10% bgcolor=#ffffff align=right>'+productNodes[i].selectSingleNode("Quantity").text+'</td>'; 
} catch (error){ 
s += '<td width=20% bgcolor=#ffffff>&nbsp;</td>'; 
} 
try{ 
s += '<td width=20% bgcolor=#ffffff align=right>'+productNodes[i].selectSingleNode("Rate").text+'</td>'; 
} catch (error){ 
s += '<td width=20% bgcolor=#ffffff>&nbsp;</td>'; 
} 

try { 
s += '<td width=20% bgcolor=#ffffff align=right>'+productNodes[i].selectSingleNode("Amount").text+'</td>'; 
} catch(error){ 
s += '<td width=20% bgcolor=#ffffff>&nbsp;</td>'; 

} 
s += '</tr>'; 
} 
try{ 
s += '<tr><td colspan=4 bgcolor=#ffffff align=right>Sales Tax %</td><td bgcolor=#ffffff align=right>'+invxml.XMLDocument.selectSingleNode('root/SalesTaxPercentage').text+'</td></tr>'; 
} catch(error){} 
try{ 
s += '<tr><td colspan=4 bgcolor=#ffffff align=right>Sales Tax Total</td><td bgcolor=#ffffff align=right>'+invxml.XMLDocument.selectSingleNode('root/SalesTaxTotal').text+'</td></tr>'; 
} catch(error){} 
try{ 
s += '<tr><td colspan=4 bgcolor=#ffffff align=right>Total</td><td bgcolor=#ffffff align=right>'+invxml.XMLDocument.selectSingleNode('root/Subtotal').text+'</td></tr>'; 
} catch(error){} 
s+='</table>'; 

document.getElementById('products').innerHTML=s; 
//alert('3'); 
} 

</script> 

<body onload="createTable()"> 
<xml id="invxml"> 
<root> 
{!AVSFQB__Invoices__c.AVSFQB__Invoice_Detail__c} 
</root> 
</xml> 
<div id="invoice"> 
<div id="company"></div> 
<table width="700" border="0"> 
<tr> 
<td> 
<b>Bill To:</b><br/> 
<div id="billto"></div> 
</td> 
<td valign="top" align="right"> 
<div id="txndate"></div> 
</td> 
</tr> 
<tr> 
<td colspan="2" align="right"> 
<div id="dataext"></div> 
</td> 
</tr> 
<tr> 
<td colspan="2" bgcolor="#cccddd"> 
<div id="products"></div> 
</td> 
</tr> 
<tr> 
<td colspan="2"> 
<div id="summary"></div> 
</td> 
</tr> 
</table> 

</div> 

<br/>&nbsp; 
(This feature is supported for IE only) <br>&nbsp;<br/>Powered by DBSync by Avankia LLC 
</body> 
</html>```

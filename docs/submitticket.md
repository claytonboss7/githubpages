---
layout: default
title: Submit an Issue
nav_order: 99
---

# Submit an Issue

<br/>
<!--  ----------------------------------------------------------------------  -->
<!--  NOTE: Please add the following <META> element to your page <HEAD>.      -->
<!--  If necessary, please modify the charset parameter to specify the        -->
<!--  character set of your HTML page.                                        -->
<!--  ----------------------------------------------------------------------  -->

<META HTTP-EQUIV="Content-type" CONTENT="text/html; charset=UTF-8">
<script src="https://www.google.com/recaptcha/api.js"></script>
<script>
 function timestamp() { var response = document.getElementById("g-recaptcha-response"); if (response == null || response.value.trim() == "") {var elems = JSON.parse(document.getElementsByName("captcha_settings")[0].value);elems["ts"] = JSON.stringify(new Date().getTime());document.getElementsByName("captcha_settings")[0].value = JSON.stringify(elems); } } setInterval(timestamp, 500); 
</script>

<!--  ----------------------------------------------------------------------  -->
<!--  NOTE: Please add the following <FORM> element to your page.             -->
<!--  ----------------------------------------------------------------------  -->

<form action="https://roadrebel--claydev.my.salesforce.com/servlet/servlet.WebToCase?encoding=UTF-8" method="POST">

<input type=hidden name='captcha_settings' value='{"keyname":"Test","fallback":"true","orgId":"00D6s0000008kFh","ts":""}'>
<input type=hidden name="orgid" value="00D6s0000008kFh">
<input type=hidden name="retURL" value="https://sfdcboss.github.io/voyajerwiki/docs/submitticket">

<!--  ----------------------------------------------------------------------  -->
<!--  NOTE: These fields are optional debugging elements. Please uncomment    -->
<!--  these lines if you wish to test in debug mode.                          -->
<!--  <input type="hidden" name="debug" value=1>                              -->
<!--  <input type="hidden" name="debugEmail"                                  -->
<!--  value="coordinator.relay.rr@gmail.com">                                 -->
<!--  ----------------------------------------------------------------------  -->

<label for="name">Contact Name</label><input  id="name" maxlength="80" name="name" size="20" type="text" /><br>

<label for="email">Email</label><input  id="email" maxlength="80" name="email" size="20" type="text" /><br>

<label for="phone">Phone</label><input  id="phone" maxlength="40" name="phone" size="20" type="text" /><br>

<label for="subject">Subject</label><input  id="subject" maxlength="80" name="subject" size="20" type="text" /><br>

<label for="description">Description</label><textarea name="description"></textarea><br>

<label for="company">Company</label><input  id="company" maxlength="80" name="company" size="20" type="text" /><br>

<label for="type">Type</label><select  id="type" name="type"><option value="">--None--</option><option value="Problem">Problem</option>
<option value="Feature Request">Feature Request</option>
<option value="Question">Question</option>
</select><br>

<label for="status">Status</label><select  id="status" name="status"><option value="">--None--</option><option value="On Hold">On Hold</option>
<option value="Escalated">Escalated</option>
<option value="Closed">Closed</option>
<option value="New">New</option>
</select><br>

<label for="reason">Case Reason</label><select  id="reason" name="reason"><option value="">--None--</option><option value="User didn&#39;t attend training">User didn&#39;t attend training</option>
<option value="Complex functionality">Complex functionality</option>
<option value="Existing problem">Existing problem</option>
<option value="Instructions not clear">Instructions not clear</option>
<option value="New problem">New problem</option>
</select><br>

<label for="priority">Priority</label><select  id="priority" name="priority"><option value="">--None--</option><option value="High">High</option>
<option value="Medium">Medium</option>
<option value="Low">Low</option>
</select><br>

<label for="currency"><span class="assistiveText">*</span>Case Currency</label><select  id="currency" name="currency"><option value="AED">AED - UAE Dirham</option>
<option value="AFN">AFN - Afghanistan Afghani (New)</option>
<option value="ALL">ALL - Albanian Lek</option>
<option value="AMD">AMD - Armenian Dram</option>
<option value="ANG">ANG - Neth Antilles Guilder</option>
<option value="AOA">AOA - Angola Kwanza</option>
<option value="ARS">ARS - Argentine Peso</option>
<option value="AUD">AUD - Australian Dollar</option>
<option value="AWG">AWG - Aruba Florin</option>
<option value="AZN">AZN - Azerbaijan Manat</option>
<option value="BAM">BAM - Convertible Marks</option>
<option value="BBD">BBD - Barbados Dollar</option>
<option value="BDT">BDT - Bangladesh Taka</option>
<option value="BGN">BGN - Bulgarian Lev</option>
<option value="BHD">BHD - Bahraini Dinar</option>
<option value="BIF">BIF - Burundi Franc</option>
<option value="BMD">BMD - Bermuda Dollar</option>
<option value="BND">BND - Brunei Dollar</option>
<option value="BOB">BOB - Bolivian Boliviano</option>
<option value="BRL">BRL - Brazilian Real</option>
<option value="BSD">BSD - Bahamian Dollar</option>
<option value="BWP">BWP - Botswana Pula</option>
<option value="BYN">BYN - Belarusian Ruble</option>
<option value="BYR">BYR - Belarusian Ruble</option>
<option value="BZD">BZD - Belize Dollar</option>
<option value="CAD">CAD - Canadian Dollar</option>
<option value="CDF">CDF - Franc Congolais</option>
<option value="CHF">CHF - Swiss Franc</option>
<option value="CLP">CLP - Chilean Peso</option>
<option value="CNY">CNY - Chinese Yuan</option>
<option value="COP">COP - Colombian Peso</option>
<option value="CRC">CRC - Costa Rica Colon</option>
<option value="CUP">CUP - Cuban Peso</option>
<option value="CVE">CVE - Cape Verde Escudo</option>
<option value="CZK">CZK - Czech Koruna</option>
<option value="DJF">DJF - Dijibouti Franc</option>
<option value="DKK">DKK - Danish Krone</option>
<option value="DOP">DOP - Dominican Peso</option>
<option value="DZD">DZD - Algerian Dinar</option>
<option value="EEK">EEK - Estonian Kroon</option>
<option value="EGP">EGP - Egyptian Pound</option>
<option value="ERN">ERN - Eritrea Nakfa</option>
<option value="ETB">ETB - Ethiopian Birr</option>
<option value="EUR">EUR - Euro</option>
<option value="FJD">FJD - Fiji Dollar</option>
<option value="GBP">GBP - British Pound</option>
<option value="GEL">GEL - Georgia Lari</option>
<option value="GHS">GHS - Ghanaian Cedi</option>
<option value="GIP">GIP - Gibraltar Pound</option>
<option value="GMD">GMD - Gambian Dalasi</option>
<option value="GNF">GNF - Guinean Franc</option>
<option value="GTQ">GTQ - Guatemala Quetzal</option>
<option value="GYD">GYD - Guyana Dollar</option>
<option value="HKD">HKD - Hong Kong Dollar</option>
<option value="HNL">HNL - Honduras Lempira</option>
<option value="HRK">HRK - Kuna</option>
<option value="HTG">HTG - Haiti Gourde</option>
<option value="HUF">HUF - Hungarian Forint</option>
<option value="IDR">IDR - Indonesian Rupiah</option>
<option value="ILS">ILS - Israeli Shekel</option>
<option value="INR">INR - Indian Rupee</option>
<option value="IQD">IQD - Iraqi Dinar</option>
<option value="IRR">IRR - Iranian Rial</option>
<option value="ISK">ISK - Iceland Krona</option>
<option value="JMD">JMD - Jamaican Dollar</option>
<option value="JOD">JOD - Jordanian Dinar</option>
<option value="JPY">JPY - Japanese Yen</option>
<option value="KES">KES - Kenyan Shilling</option>
<option value="KGS">KGS - Kyrgyzstan Som</option>
<option value="KHR">KHR - Cambodia Riel</option>
<option value="KPW">KPW - North Korean Won</option>
<option value="KRW">KRW - Korean Won</option>
<option value="KWD">KWD - Kuwaiti Dinar</option>
<option value="KYD">KYD - Cayman Islands Dollar</option>
<option value="KZT">KZT - Kazakhstan Tenge</option>
<option value="LAK">LAK - Lao Kip</option>
<option value="LBP">LBP - Lebanese Pound</option>
<option value="LKR">LKR - Sri Lanka Rupee</option>
<option value="LRD">LRD - Liberian Dollar</option>
<option value="LSL">LSL - Lesotho Loti</option>
<option value="LYD">LYD - Libyan Dinar</option>
<option value="MAD">MAD - Moroccan Dirham</option>
<option value="MDL">MDL - Moldovan Leu</option>
<option value="MGA">MGA - Malagasy Ariary</option>
<option value="MKD">MKD - Macedonian Denar</option>
<option value="MMK">MMK - Myanmar Kyat</option>
<option value="MNT">MNT - Mongolian Tugrik</option>
<option value="MOP">MOP - Macau Pataca</option>
<option value="MRO">MRO - Mauritanian Ougulya</option>
<option value="MUR">MUR - Mauritius Rupee</option>
<option value="MVR">MVR - Maldives Rufiyaa</option>
<option value="MWK">MWK - Malawi Kwacha</option>
<option value="MXN">MXN - Mexican Peso</option>
<option value="MYR">MYR - Malaysian Ringgit</option>
<option value="MZN">MZN - Mozambique New Metical</option>
<option value="NAD">NAD - Namibian Dollar</option>
<option value="NGN">NGN - Nigerian Naira</option>
<option value="NIO">NIO - Nicaragua Cordoba</option>
<option value="NOK">NOK - Norwegian Krone</option>
<option value="NPR">NPR - Nepalese Rupee</option>
<option value="NZD">NZD - New Zealand Dollar</option>
<option value="OMR">OMR - Omani Rial</option>
<option value="PAB">PAB - Panama Balboa</option>
<option value="PEN">PEN - Peruvian Sol</option>
<option value="PGK">PGK - Papua New Guinea Kina</option>
<option value="PHP">PHP - Philippine Peso</option>
<option value="PKR">PKR - Pakistani Rupee</option>
<option value="PLN">PLN - Polish Zloty</option>
<option value="PYG">PYG - Paraguayan Guarani</option>
<option value="QAR">QAR - Qatar Rial</option>
<option value="RON">RON - Romanian Leu</option>
<option value="RSD">RSD - Serbian Dinar</option>
<option value="RUB">RUB - Russian Rouble</option>
<option value="RWF">RWF - Rwanda Franc</option>
<option value="SAR">SAR - Saudi Arabian Riyal</option>
<option value="SBD">SBD - Solomon Islands Dollar</option>
<option value="SCR">SCR - Seychelles Rupee</option>
<option value="SDG">SDG - Sudanese Pound</option>
<option value="SEK">SEK - Swedish Krona</option>
<option value="SGD">SGD - Singapore Dollar</option>
<option value="SLL">SLL - Sierra Leone Leone</option>
<option value="SOS">SOS - Somali Shilling</option>
<option value="SRD">SRD - Surinam Dollar</option>
<option value="STD">STD - São Tomé and Príncipe Dobra</option>
<option value="SYP">SYP - Syrian Pound</option>
<option value="SZL">SZL - Swaziland Lilageni</option>
<option value="THB">THB - Thai Baht</option>
<option value="TJS">TJS - Tajik Somoni</option>
<option value="TMT">TMT - Turkmenistan New Manat</option>
<option value="TND">TND - Tunisian Dinar</option>
<option value="TOP">TOP - Tonga Pa&#39;anga</option>
<option value="TRY">TRY - Turkish Lira (New)</option>
<option value="TTD">TTD - Trinidad&amp;Tobago Dollar</option>
<option value="TWD">TWD - Taiwan Dollar</option>
<option value="TZS">TZS - Tanzanian Shilling</option>
<option value="UAH">UAH - Ukraine Hryvnia</option>
<option value="UGX">UGX - Ugandan Shilling</option>
<option value="USD" selected="selected">USD - U.S. Dollar</option>
<option value="UYU">UYU - Uruguayan Peso</option>
<option value="UZS">UZS - Uzbekistan Sum</option>
<option value="VES">VES - Venezuelan Bolívar Soberano</option>
<option value="VND">VND - Vietnam Dong</option>
<option value="VUV">VUV - Vanuatu Vatu</option>
<option value="WST">WST - Samoa Tala</option>
<option value="XAF">XAF - CFA Franc (BEAC)</option>
<option value="XCD">XCD - East Caribbean Dollar</option>
<option value="XOF">XOF - CFA Franc (BCEAO)</option>
<option value="XPF">XPF - Pacific Franc</option>
<option value="YER">YER - Yemen Riyal</option>
<option value="ZAR">ZAR - South African Rand</option>
<option value="ZMW">ZMW - Zambian Kwacha (New)</option>
<option value="ZWL">ZWL - Zimbabwe Dollar</option>
</select><br>

<input type="hidden"  id="external" name="external" value="1" /><br>

<div class="g-recaptcha" data-sitekey="123"></div><br>
<input type="submit" name="submit">

</form>


**Is your feature request related to a problem? Please describe.**
A clear and concise description of what the problem is. Ex. I'm always frustrated when [...]

**Describe the solution you'd like**
A clear and concise description of what you want to happen.

**Describe alternatives you've considered**
A clear and concise description of any alternative solutions or features you've considered.

**Additional context**
Add any other context or screenshots about the feature request here.

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

<label for="subject">Subject</label><br/><input  id="subject" maxlength="80" name="subject" size="20" type="text" /><br>

<label for="description">Description</label><br/><textarea name="description"></textarea><br>

<label for="type">Type</label><select  id="type" name="type"><option value="">--None--</option><option value="Problem">Problem</option>
<option value="Feature Request">Feature</option>
<option value="Question">Question</option>
<option value="Bug">Bug</option>
</select><br>
<input type="hidden"  id="external" name="external" value="1" /><br>

<div class="g-recaptcha" data-sitekey="123"></div><br>
<input type="submit" name="submit">
<br/>
<br/>
<br/>
**Is your feature request related to a problem? Please describe.**

A clear and concise description of what the problem is. Ex. I'm always frustrated when [...]
<label for="subject">Subject</label><br/><input  id="subject" maxlength="80" name="subject" size="20" type="text" /><br>

**Describe the solution you'd like**

A clear and concise description of what you want to happen.
<label for="description">Description</label><br/><textarea name="description"></textarea><br>


</form>
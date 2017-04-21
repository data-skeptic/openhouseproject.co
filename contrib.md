---
layout: default
title: Contributing 
permalink: /contributing/
---

### Contributing

The first step is to drop by our Slack channel and introduce yourself! You can sign up at [https://dataskeptic.com/contact-us](https://dataskeptic.com/contact-us).  Tell us about who you are and what your interest in the project is.  If you'd like to develop a new skill, we're happy to help provide some training.

Open technical low(ish) hanging fruit can be found [here](https://waffle.io/data-skeptic/home-data-gallery)

Our tasks related to product management, graphic design, and engineering leadership can be found [here](https://trello.com/b/KsxRcumo/openhouse-roadmap-choices).

<script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
<script>
  function submit() {
    var api = "https://5xwvsgjnqi.execute-api.us-east-1.amazonaws.com/prod/OH-submit-url"
    var email = $("#email").val()
    var url = $("#url").val()
    var c = $("#cb_notify").attr('checked')
    var checked = true
    if (c == undefined) {
      checked = false
    }
    var res = {"email": email, "url": url, "checked": checked}
    $("#error").hide() 
    $("#thanks").hide()
    $("#waiting").show()
    $.ajax({
      url: api,
      type: 'POST',
      contentType: 'text/json',
      dataType: 'json',
      data: JSON.stringify(res),
      success: function (resp) {
        $("#waiting").hide()
        $("#thanks").show()
      },
      error: function (xhr, ajaxOptions, thrownError) {
        $("#error").show()
        $("#waiting").hide()
      }
    })
  }

$( document ).ready(function() {
  $("#error").hide()
  $("#waiting").hide()
  $("#thanks").hide()
})
</script>


<style>
.box {
  width:300px;
}
#btnSubmit {
  padding: 10px;
}
#urlbox {
  margin-top: 5px;
  margin-bottom: 10px;
  padding: 5px;
  border-style: solid;
  border-width: 1px;
  border-color: #999;
  border-radius: 4px;
}
.alertbox {
  width: 325px;
  margin-top: 10px;
  padding: 10px;
  border-style: solid;
  border-width: 2px;
  border-color: #000;
  border-radius: 4px;
  text-align: center;
}
#waiting {
  background-color: #eef;
}
#thanks {
  background-color: #efe;
}
#error {
  background-color: #fee;  
}
</style>

Looking to make a one-time contribution.  Consider helping in one of the three ways below.

<div id="urlbox">
 <h3>1) Tell us about a website</h3>

  <table>
    <tr>
      <td>Email:</td>
      <td><input id="email" class="box" type="text" value=""></td>
    </tr>
    <tr>
      <td>URL:</td>
      <td><input id="url" class="box" type="text" value="http://"></td>
    </tr>
    <tr>
      <td></td>
      <td><input type="checkbox" id="cb_notify" checked />Notify me about updates related to this data</td>
    </tr>
    <tr>
      <td></td>
      <td align="right">
      	<button id="btnSubmit" onclick="submit()">Submit</button>
      </td>
    </tr>
  </table>

  <div class="alertbox" id="error">An error has occured.  That stinks!  I guess just email <a href="mailto:kyle@dataskeptic.com">kyle@dataskeptic.com</a>.  Send him your recommended URL and comment on how ashamed he should be that the site is broken.</div>
  <div class="alertbox" id="waiting">Submitting...</div>
  <div class="alertbox" id="thanks">Thanks</div>

</div>

2) Help us review pages that we've crawled to validate if they should be parsed or not by using our web interface found [here](http://openhouseproject.co/review-crawls.html).

3) Help us develop parsing code.  Get started in 2 minutes using our web interface found [here](http://openhouseproject.co/create-parse.html).


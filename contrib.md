---
layout: default
title: Contributing 
permalink: /contributing/
---

### Contributing

If you'd like to participate, please email kyle@dataskeptic.com and ask to join our Slack channel.

**Join us for a live chat discussion of the project every Tuesday at 6:30pm PST in the Data Skeptic Slack channel.**

The first step is to drop by our Slack channel and introduce yourself! Tell us about who you are and what your interest in the project is. 

Open tasks you can volunteer for can be found on our waffle.io boards for the 
<a href="https://waffle.io/data-skeptic/home-data-api">API</a> and the
<a href="https://waffle.io/data-skeptic/home-data-gallery">Interactive tool</a>.
If you're not looking to contribute technical skills but still want to help out,
check out our list of 
<a href="https://trello.com/b/QPhASWc9/openhouse-non-technical-tasks">non-technical volunteer tasks</a>.

<iframe width="560" height="315" src="https://www.youtube.com/embed/cHoRn1UxEzk" frameborder="0" allowfullscreen></iframe>

### Tell us about a website


<script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
<script>
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
      success: function (resp) {
        $("#waiting").hide()
        $("#thanks").hide()
      },
      error: function (xhr, ajaxOptions, thrownError) {
        $("#error").show()
        $("#waiting").hide()
      }
    })
  }
</script>




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
      <td colspan="2" align="right">
      	<button id="btnSubmit" onclick="submit()">Submit</button>
      </td>
    </tr>
  </table>

  <div class="alertbox" id="error">An error has occured.  That stinks!  I guess just email <a href="mailto:kyle@dataskeptic.com">kyle@dataskeptic.com</a>.  Send him your recommended URL and comment on how ashamed he should be that the site is broken.</div>
  <div class="alertbox" id="waiting">Submitting...</div>
  <div class="alertbox" id="thanks">Thanks</div>



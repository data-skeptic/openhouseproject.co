---
layout: default
title: Sign Up
permalink: /signup/
---

# Account creation

Some requests to our API require an account.  While the API can also be called for some purposes without authenticating, we appreciate it if you create an account so we can better capture metadata about usage.

You can get a free account by signing up using the form below.

<script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>

<table>
    <tr><td>Username:</td><td><input type="text" id="username" hint="username" /></td><td><div class='errField' id='usernameErr'></div></td></tr>
    <tr><td>Password:</td><td><input type="password" id="password" hint="Password" /></td><td><div class='errField' id='passwordErr'></div></td></tr>
    <tr><td>Email:</td><td><input type="email" id="email" hint="Email Address" /></td><td><div class='errField' id='emailErr'></div></td></tr>
    <tr><td></td><td><button id="btnSignUp">Signup</button></td></tr>
</table>

<div id='msg'></div>
<div id='wait'></div>

Already have an account?  Check out this
[Jupyter notebook](https://github.com/data-skeptic/api-connector/blob/master/python/Push%20and%20Fetch%20Data%20Example.ipynb)
that shows how to interact with the API.

<script>
function showWaiting(show=true) {
	if (show) {
		$("#wait").html("Wait...")
		$("#wait").show()
		$("#btnSignUp").prop("disabled",true)
	}
	else {
		$("#wait").hide()
		$("#btnSignUp").prop("disabled",false)
	}
}

$(document).ready(function() {
	$(btnSignUp).click(function() {
		request = {
			'username': $("#username").val()
		,	'password': $("#password").val()
		,	'first_name': $("#first_name").val()
		,	'last_name': $("#last_name").val()
		,	'email': $("#email").val()
		}
		showWaiting(true)
		$("#msg").hide()
		$(".errField").hide()
		console.log(JSON.stringify(request))
		$.ajax({
			type: 'POST',
			url: 'http://api.openhouseproject.co/api/signup/',
			data: JSON.stringify(request),
			contentType: "application/json",
			success: function(data) {
				console.log(data)
				showWaiting(false)
				$("#msg").html("Account created successfully!  Please check your email for a confirmation link.")
				$("#msg").show()
			},
			error: function (request, status, error) {
				console.log(request)
				var errMsg = "Signup failed."
				rt = request['responseText']
				if (rt !== undefined) {
					rt = JSON.parse(rt)
					keys = Object.keys(rt)
					$.each(keys, function(i, key) {
						var elem = "#" + key + "Err"
						$(elem).html(rt[key].toString())
						$(elem).show()
					})
				}
				showWaiting(false)
				$("#msg").html(errMsg)
				$("#msg").show()
		    }
		});
	})
});
</script>

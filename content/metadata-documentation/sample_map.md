---
title: Sample Map
author: Jessica Chung
date: '2018-06-05'
slug: sample-map
categories: []
tags: []
weight: 4
description: 'Interactive map of sample data in Mediaflux.'
---

Enter the password to view the interactive map of the sample data in the 
Hoffmann Lab Mediaflux project.

<!-- 

https://github.com/matteobrusa/Password-protection-for-static-pages

Input a string, hash it, then try to access map using the hash as part of the URL.

But can't check if URL is successful since it requires on checking status codes
across domains. After password is entered, load URL in new window and if the
password is incorrect, just lead to a 'Page Not found' page.

-->

<div style="width: 400px; height: 200px; margin:auto; margin-top:50px; text-align:center">				
  <input style="text-align: center" id="password" type="password" placeholder="Password" />
  <button id="loginbutton" type="button" style="padding: 15px 30px; color: white; background-color: #008CBA; border-radius: 8px; margin:auto">Enter</button>
</div>

<script type="text/javascript" src="https://code.jquery.com/jquery-1.12.0.min.js"></script>
<script type="text/javascript" src="https://rawcdn.githack.com/chrisveness/crypto/7067ee62f18c76dd4a9d372a00e647205460b62b/sha1.js"></script>

<script type="text/javascript">
	"use strict";
	
	function loadPage(pwd) {
		var hash = pwd;
		hash = Sha1.hash(pwd);
		var url = "http://45.113.232.220/secret/" + hash + "/sample_map.html";
    window.open(url, '_blank');
	}
	
	$("#loginbutton").on("click", function() {
		loadPage($("#password").val());
	});
	
	$("#password").keypress(function(e) {
		if (e.which == 13) {
			loadPage($("#password").val());
		}
	});
	
	$("#password").focus();
	
	$(document).ready(function() {
	  $("#loginbutton").hover(function() {
	    $(this).css("background-color", "#2E53A5");
	  }, function() {
	    $(this).css("background-color", "#008CBA");
	  });
  });
	
</script>


Last updated 2018-09-07.
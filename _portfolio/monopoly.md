--- 
title: 'Monopoly test' 
date: 2020-08-17 
permalink: /portfolio/2020/08/Monopoly/ 
---
<h1>My First Web Page</h1>
<p>My First Paragraph</p>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script type="text/javascript">
$.get("https://ipinfo.io/json", function (response) {
    $("#ip").html("IP: " + response.ip);
    $("#address").html("Location: " + response.city + ", " + response.region);
    $("#details").html(JSON.stringify(response, null, 4));
}, "jsonp");

</script>


<h3>Client side IP geolocation using <a href="http://ipinfo.io">ipinfo.io</a></h3>

<hr/>
<div id="ip"></div>
<div id="address"></div>
<hr/>Full response: <pre id="details"></pre>


<div id="details"></div>
--- 
title: 'Monopoly test' 
date: 2020-08-17 
permalink: /portfolio/2020/08/Monopoly/ 
---


<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script type="text/javascript">
$.get("https://ipinfo.io/json", function (response) {
    $("#ip").html("IP: " + response.ip);
    $("#address").html("Location: " + response.city + ", " + response.region);
    $("#loc").html("IP: " + response.loc);
    $("#details").html(JSON.stringify(response, null, 4));
}, "jsonp");

</script>

<h3>Client side IP geolocation using <a href="http://ipinfo.io">ipinfo.io</a></h3>

<hr/>
<div id="ip"></div>
<div id="address"></div>
<div id="loc"></div>

<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"></script>
<link href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css" rel="stylesheet"/>
<div id="osm-map"></div>
<script>// Where you want to render the map.
      var element = document.getElementById('osm-map');
      element.style = 'height:300px;';
      var map = L.map(element);
      L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);
      var target = L.latLng(52.3008,4.8639);
      map.setView(target, 14);
      L.marker(target).addTo(map);
</script>

Full Response:
<div id="details"></div>
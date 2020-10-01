--- 
title: 'Show My Ip' 
date: 2020-09-30 
permalink: /portfolio/2020/09/my-ip/ 
---


<h3>Client side IP geolocation using <a href="http://ipinfo.io">ipinfo.io</a></h3>


<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>

<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"></script>
<link href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css" rel="stylesheet"/>
<div id="osm-map"></div>
<script>// Where you want to render the map.
var long_lat;
$.get("https://ipinfo.io/json", function (response) {
    $("#ip").html("IP: " + response.ip);
    $("#address").html("Location: " + response.city + ", " + response.region);
    long_lat = (response.loc);
    $("#details").html(JSON.stringify(response, null, 4));
}, "jsonp");
setTimeout(() => {
var element = document.getElementById('osm-map');
      element.style = 'height:300px;';
      var map = L.map(element);
      L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);
      var target = L.latLng(long_lat.split(','));
      map.setView(target, 14);
      L.marker(target).addTo(map);
}, 150); //Wait 150 ms plotting to get json object.

</script>

# Location Details
<div id="ip"></div>
<div id="address"></div>
<div id="loc"></div>

Full Response:
<div id="details"></div>

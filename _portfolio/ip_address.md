--- 
title: 'Show My Ip' 
date: 2020-09-30 
permalink: /portfolio/2020/09/my-ip/ 
---
Basic script with which users can check their location. IP-addresses and geolocations are gathered from [http://ipinfo.io] and are displayed with the help of Leaflet's open-streetmap source ([https://leafletjs.com/]).

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script>
$.get("https://ipinfo.io/json", function (response) {
    $("#ip").html("IP: " + response.ip);
    $("#address").html("Location: " + response.city + ", " + response.region);
    long_lat = (response.loc);
    $("#loc").html(response.loc);
    $("#details").html(JSON.stringify(response, null, 4));
}, "jsonp");
</script>
# Location Details
**User's IP-Address and other features are extracted from [http://ipinfo.io].**
<div id="ip"></div>
<div id="address"></div>
<div id="loc"></div>

Full Response:
<div id="details"></div>


# Your Location
Moreover, the location of a user's IP-address is displayed on a map. Note that the location may be incorrect, due to the absence of exact location determination. 
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"></script>
<link href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css" rel="stylesheet"/>
<div id="osm-map"></div>
<script>
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
}, 4000); //Wait 1500 ms plotting to get json object.

</script>




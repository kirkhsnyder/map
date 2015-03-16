# map
<head>
 
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<title>Mapa</title>
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<link href="http://api.tiles.mapbox.com/mapbox.js/v1.5.0/mapbox.css" media="screen, print" rel="stylesheet">
<script src="http://api.tiles.mapbox.com/mapbox.js/v1.5.0/mapbox.js"></script>
<style type="text/css">
/* paste CSS below this line */
#map {
  width:400px;
  height:400px;
}
</style>
</head>
<body>
<!-- paste HTML below this line -->
<div id="map"></div> 
<script type="text/javascript">
// paste JavaScript below this line
// 1817 map attribution
var attribution_1817 = 'Map image from <a href="http://maps.nypl.org/warper">NYPL Map Warper</a>';
 
// 1817 tile set with attribution
var nyc_1817 = L.tileLayer(  'http://maps.nypl.org/warper/maps/tile/15128/{z}/{x}/{y}.png' , { attribution: attribution_1817 } );
 
// 2014 tile set attribution
var attribution_2014 = 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, Imagery © <a href="http://mapbox.com">Mapbox</a>';

// 2014 tile set using MapBox ID (replace with your own)
var nyc_2014 = L.tileLayer( 'https://{s}.tiles.mapbox.com/v3/{id}/{z}/{x}/{y}.png',{id: 'examples.map-20v6611k',attribution: attribution_2014});
 
// create the map with the default the tileset
var map = L.map('map', {layers:nyc_1817});
 
// create a variable to hold all tile sets and name them so we can use it for the toggler
var baseMaps = {
  "New York 2014": nyc_2014,
  "New York 1817": nyc_1817
};

// the geojson as it comes from the text document
var geostring = '{"type":"FeatureCollection","features":[{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Josiah R. Brady","Address":"18 Jay St","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00991976261139,40.71781037496519]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"William Bridges","Address":"47 Walker St","Occupation":"Architect and City Surveyor"},"geometry":{"type":"Point","coordinates":[-74.00368630886078,40.718936609188304]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Samuel Clark","Address":"Corner of Elm (Lafayette) and Grand","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-73.99900585412979,40.71987376790721]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"John J. Holland","Address":"45 Sugarloaf St (Franklin)","Occupation":"Artist and Architect"},"geometry":{"type":"Point","coordinates":[-74.00242030620575,40.71675527543749]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Edward Probyn","Address":"12 Vandewater St","Occupation":"Architect and Builder"},"geometry":{"type":"Point","coordinates":[-74.0022325515747,40.71073539932408]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Ezra Weeks","Address":"16 Harrison St","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00968104600906,40.71889595124461]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"John McComb","Address":"Bowery-hill","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00618076324463,40.708295578231315]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Josiah R. Brady","Address":"18 Jay St","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00991976261139,40.71781037496519]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"William Bridges","Address":"47 Walker St","Occupation":"Architect and City Surveyor"},"geometry":{"type":"Point","coordinates":[-74.00368630886078,40.718936609188304]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Samuel Clark","Address":"Corner of Elm (Lafayette) and Grand","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-73.99900585412979,40.71987376790721]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"John J. Holland","Address":"45 Sugarloaf St (Franklin)","Occupation":"Artist and Architect"},"geometry":{"type":"Point","coordinates":[-74.00242030620575,40.71675527543749]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Edward Probyn","Address":"12 Vandewater St","Occupation":"Architect and Builder"},"geometry":{"type":"Point","coordinates":[ -74.0022325515747,40.71073539932408]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"Ezra Weeks","Address":"16 Harrison St","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00968104600906,40.71889595124461]}},{"type":"Feature","properties":{"marker-color":"#7e7e7e","marker-size":"medium","marker-symbol":"","Name":"John McComb","Address":"Bowery-hill","Occupation":"Architect"},"geometry":{"type":"Point","coordinates":[-74.00618076324463,40.708295578231315]}}]}';


// parse the geojson string to a proper json structure
var geodata = JSON.parse(geostring);
 
// now make it understandable by leaflet
var geolayer = L.geoJson(geodata, {onEachFeature: showPopup});
 
// add the points to the map
geolayer.addTo(map);
 
// zoom the map to the bounds of the points
map.fitBounds(geolayer.getBounds());

// a data layers variable for the toggler
var overlays = {
    "Architects": geolayer
}
// add the tile set switcher control
L.control.layers(baseMaps, overlays).addTo(map);
function showPopup(feature, layer) {
  var key, val;
  var content = [];
  for (key in feature.properties) {
    val = feature.properties[key];
    content.push("<strong>" + key + ":</strong> " + val);
  }
  layer.bindPopup(content.join("<br />"));
}



</script>
</body>
</html>



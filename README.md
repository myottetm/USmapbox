# USmapbox

//I'm a researcher at the Institute on Metropolitan Opportunity trying
//to share a html file that interfaces with MapBox:

<!DOCTYPE html>
<html>
<head>
  <meta charset='utf-8' />
  <title>Display a map</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/v0.46.0/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v0.46.0/mapbox-gl.css' rel='stylesheet' />
  <style>
    body { margin:0; padding:0; }
    h2,
h3 {
  margin: 10px;
  font-size: 1.2em;
}

h3 {
  font-size: 1em;
}

p {
  font-size: 0.85em;
  margin: 10px;
  text-align: left;
}
    #map { position:absolute; top:0; bottom:0; width:100%; }
    /**
    * Set rules for how the map overlays
    * (info box and legend) will be displayed
    * on the page. */
    .map-overlay {
      position: absolute;
      bottom: 0;
      right: 0;
      background: rgba(255, 255, 255, 0.8);
      margin-right: 20px;
      font-family: Arial, sans-serif;
      overflow: auto;
      border-radius: 3px;
    }

    #features {
      top: 0;
      height: 70px;
      margin-top: 10px;
      width: 450px;
    }

    #legend {
      padding: 5px;
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
      line-height: 18px;
      height: 300px;
      margin-bottom: 40px;
      width: 190px;
    }

    .legend-key {
      display: inline-block;
      border-radius: 20%;
      width: 10px;
      height: 10px;
      margin-right: 20px;
    }
    .mapboxgl-popup {
      max-width: 400px;
      font: 12px/20px 'Helvetica Neue', Arial, Helvetica, sans-serif;
  }
  </style>
</head>
<body>

<div id='map'></div>
<div class='map-overlay' id='legend'><p><b>Net Change in Number<br>of Low Income Persons</b></p></div>
<div class='map-overlay' id='features'><h2>Gentrification and Low Income Concentration<br>in U.S. Census Tracts, 2000 to 2016</h2></div>

<script>
mapboxgl.accessToken = 'pk.eyJ1IjoibXlvdHRldG0iLCJhIjoiY2psem4xMWJxMjNlcDN2cDQxd25tMDNhMCJ9.Hn5l5XlTMzKQv_m2lg394Q';
const map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/myottetm/cjlz7h54v01cz2rp0m5k80qqv',
  center: [-94.558443, 38.464226],
  zoom: 4.3
});
map.on('load', function() {
  // the rest of the code will go in here
  var layers = ['< -1,400', '-1,400 to -1,050', '-1,050 to -700', '-700 to -350', '-350 to -1', 'None', '1 to 350', '350 to 700','700 to 1,050','1,050 to 1,400','> 1,400','','Non-Metro Area'];
var colors = ['#002673', '#0067E6', '#26A6FF', '#80D9FF', '#CCF2FF', '#FFFFFF', '#FFE6BF', '#FFB399', '#FF804D', '#FF0000', '#730000','#f2f2f2','#C0C0C0'];
for (i = 0; i < layers.length; i++) {
  var layer = layers[i];
  var color = colors[i];
  var item = document.createElement('div');
  var key = document.createElement('span');
  key.className = 'legend-key';
  key.style.backgroundColor = color;

  var value = document.createElement('span');
  value.innerHTML = layer;
  item.appendChild(key);
  item.appendChild(value);
  legend.appendChild(item);
}
map.addLayer({
       'id': 'CensusTracts',
       'type': 'fill',
       'source': {
           'type': 'vector',
           'url': 'mapbox://myottetm.dsir2wpp'
   //},
  // 'source-layer': 'US_tract10i-b9dicn'
         }
    });

   // When a click event occurs on a feature in the states layer, open a popup at the
   // location of the click, with description HTML from its properties.
   map.on('click', 'CensusTracts', function (e) {
       new mapboxgl.Popup()
           .setLngLat(e.lngLat)
           .setHTML(e.features[0].properties.ChngLow2)
           .addTo(map);
   });
////////////point and click on tracts, pull up variables, change variable names.
   // Change the cursor to a pointer when the mouse is over the states layer.
map.getCanvas().style.cursor = 'default';
   });
//});
</script>

</body>
</html




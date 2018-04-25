<!DOCTYPE html>
<html>
  <head>
    <title>EPSG:4326</title>
    <link rel="stylesheet" href="https://openlayers.org/en/v4.6.5/css/ol.css" type="text/css">
    <!-- The line below is only needed for old environments like Internet Explorer and Android 4.x -->
    <script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=requestAnimationFrame,Element.prototype.classList,URL"></script>
    <script src="https://openlayers.org/en/v4.6.5/build/ol.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/proj4js/2.4.4/proj4.js"></script>
  </head>
  <body>
    <div id="map" class="map"></div>
    <script>

      proj4.defs('EPSG:32633', '+proj=utm +zone=33 +datum=WGS84 +units=m +no_defs');
      var proj32633 = ol.proj.get('EPSG:32633');
      proj32633.setExtent([-100205, 6300205, 1249795, 7950205]);

var map = new ol.Map({
  target: 'map',
  layers: [
    new ol.layer.Tile({
      source: new ol.source.TileWMS({
        url: 'http://localhost:5000/rasdaman/ows',
        params: {
          LAYERS: 'DTM',
          TRANSPARENT: false,
          VERSION: '1.3.0'
        }
      })
    })
  ],
  view: new ol.View({
    // Long, Lat
    center: [-8421, 6524185],
    minZoom: 5,
    maxZoom: 10,
    zoom: 7,
    projection: 'EPSG:32633'
  })
});

map.addControl(new ol.control.MousePosition({
  target: 'position'
}));
    </script>
  </body>
</html>

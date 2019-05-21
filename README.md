# Hexagonal Density Map

### This project focuses on the creation of a hexagonal density map of U.S. Superfund sites via <a href="https://d3js.org/">D3</a> and <a href="https://leafletjs.com/">Leaflet</a>. Superfund data utilized for this map originated from the <a href="https://data.noaa.gov/dataset/dataset/superfund-sites">U.S. National Oceanic and Atmospheric Administration's Superfund Sites database</a> and map tiles by Carto via <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>.

#### Now, to go through the important portions of the code in the index file:

##### Styling

Map placeholder

```
  <style> 
    html,
    body, #map { width: 100%; height: 100%; margin: 0; background: #fff}
    i {
      width: 0.5px;
       height: 16px;
       float: right;
       opacity: 0.7;
      }
  </style>
  
```
Setting Hexagons + Hover/Tooltips
```
   .hexbin-hexagon { 
      stroke: #000;
      stroke-width: 1px;
     }
   .hexbin-container:hover .hexbin-hexagon {
      transition: 200ms;
      stroke: limegreen;
      stroke-width: 5px;
      stroke-opacity: 1;
     }
    .hexbin-tooltip {
      padding: 8px;
      border-radius: 4px;
      border: 1px solid black;
      background-color: white;
     }
```
Setting Info Box + Legend
```
    .info {
      padding: 6px 8px;
      font: 14px/16px Arial, Helvetica, sans-serif;
      background: white;
      background: rgba(255,255,255,0.8);
      box-shadow: 0 0 15px rgba(0,0,0,0.2);
      border-radius: 5px;
    }
    .legend {
      background-color: "black";
      line-height: 25px;
      color: #555;
      width: auto;
    }
    .legend i {
      width: 18px;
      height: 18px;
      float: left;
      margin-right: 8px;
      opacity: 0.7;
    }
```
Setting Colors, Range, and Options for Hexagons
```javascript
var colorRange = [ 'yellow', 'orange', 'red', 'blue', 'purple' ];
var colorScale = d3.scaleLinear().domain([1,2,3,4,5]).range(colorRange);
var options = {
    radius : 12, //Hexagon maximum radius
    opacity: 0.5,
    duration: 500,
    colorRange: colorRange,
    colorScaleExtent: [1, 5]
   };
```
Setting Map Center, Tilelayer, and Creating Map
```javascript
var center = [39.8, -98.5]; //Map Center
var osmUrl = 'https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png',
    osmAttrib = '  Map tiles by Carto, under CC BY 3.0. Data by &copy <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>,     under ODbL.',
    osm = L.tileLayer(osmUrl, {maxZoom: 18, attribution: osmAttrib}); //Tilelayer
mymap = new L.Map('map', {layers: [osm], center: new L.LatLng([35.7], [-98]), zoom: 4}); // Creating map
```


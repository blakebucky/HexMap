<a href="https://github.com/Asymmetrik/leaflet-d3">Asymmetrik D3.js Hexbin Tutorial</a>

<a href="http://projects.delimited.io/experiments/hexbins/starbucks.html">Hexin example using a CSV file (devtools)</a>
# Hexagonal Density Map

### This project focuses on the creation of a hexagonal density map of U.S. Superfund sites via <a href="https://d3js.org/">D3</a> and <a href="https://leafletjs.com/">Leaflet</a>. Superfund data utilized for this map originated from the <a href="https://data.noaa.gov/dataset/dataset/superfund-sites">U.S. National Oceanic and Atmospheric Administration's Superfund Sites database</a> and map tiles by Carto via <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>.

#### Now, to go through the important portions of the code in the index file:

##### Styling

Map Base Styling (HTML)

```
    html,
    body, #map { width: 100%; height: 100%}
    i {
      width: 0.5px;
       height: 16px;
       float: right;
       opacity: 0.7;
      }
  
```
Setting Hexagons + Hover/Tooltips (Start of CSS)
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
Setting Info Box + Legend (End of CSS)
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
JavaScript (Leaflet + D3)
Setting Colors, Range, + Options for Hexagons
```javascript
var colorRange = [ 'yellow', 'orange', 'red', 'blue', 'purple' ];
var colorScale = d3.scaleLinear().domain([1,2,3,4,5]).range(colorRange);
var options = {
    radius : 12, //Hexagon maximum radius
    opacity: 0.5,
    colorRange: colorRange,
    colorScaleExtent: [1, 5]
   };
```
Setting Map Center, Tilelayer, + Creating Map
```javascript
var center = [39.8, -98.5]; //Map Center
var osmUrl = 'https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png',
    osmAttrib = '  Map tiles by Carto, under CC BY 3.0. Data by &copy <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>, under ODbL and <a href="https://data.noaa.gov/dataset/dataset/superfund-sites">NOAA</a>.',
    osm = L.tileLayer(osmUrl, {maxZoom: 18, attribution: osmAttrib}); //Tilelayer
mymap = new L.Map('map', {layers: [osm], center: new L.LatLng([35.7], [-98]), zoom: 4}); // Creating map
```
Creating Hexbins, Adding them to Map, + Applying Options to Hexbins on Map
```javascript
var hexLayer = L.hexbinLayer(options).addTo(mymap)
	.hoverHandler(L.HexbinHoverHandler.compound({  //Applying hovering
				handlers: [
					L.HexbinHoverHandler.resizeFill(),
					L.HexbinHoverHandler.tooltip() 
				]
			}));
hexLayer
	.radiusRange([5, 12])  //Setting range of values of hexagon radii
	.lng(function(d) { return d[0]; })  //Setting longitude for each hex
	.lat(function(d) { return d[1]; })  //Setting latitude for each hex
	.colorValue(function(d) { return d.length; })  //Setting color for each hex
	.radiusValue(function(d) { return d.length; });  //Setting radius for each hex
```
Defining Superfund Sites via Longitude/Latitude + Calling Data
```javascript
var pointData = function(){
    var data = [];
    hexLayer.data([[lat1,lon1]...[latN,lonN]  //Full lat/lon can be found in index file
    ]);
};
pointData();
```
Creating Function to Generate Legend Colors
```javascript
function getColor(d) {   //Categorical colors; can also create function to assign color based on continuous values
        return d === 1 ? "yellow" :
               d === 2 ? "orange" :
               d === 3 ? "red" :
               d === 4 ? "blue" :
               d >= 5 ? "purple":
                        "purple"
                          ;
    }
```
Creating Legend + Assigning Categories/Colors
```javascript
    var legend = L.control({position: 'bottomright'});
        legend.onAdd = function (map) {
    var div = L.DomUtil.create('div', 'info legend');  //creating new div for legend
       labels = ['<strong>Superfund Site Density Categories</strong>'],   //Legend title
       categories = [1,2,3,4,'5 or more sites'];  //Legend categories
       for (var i = 0; i < categories.length; i++) {  //for loop assigning colors + categories
               div.innerHTML +=
               labels.push(
                   '<i style="background:' + getColor(categories[i]) + '"></i> ' +
                   (categories[i] ? categories[i] : '+'));
           }
           div.innerHTML = labels.join('<br>');
	   div.innerHTML += '<hr><img src="img/Hexagon.svg" alt="hex" style="width:70px;height:70px;"></img><em>Larger Hexagons = Higher Density</em>'
       return div;
    };
    legend.addTo(mymap);
```
Creating Info Box
```javascript
  var info = L.control();
    info.onAdd = function (mymap) {
        this._div = L.DomUtil.create('div', 'info'); // create a div for info box
        this.update();
        return this._div;
    };
    info.update = function (props) {
        this._div.innerHTML = '<h3><u>U.S. Superfund Site Hexagonal Map</u></h3>' + '<h4>Superfund sites are locations in the U.S. with extensive </br> environmental contamination that the federal government </br> has designated for cleanup fund allocation.</h4>' + 'Data Source: U.S. Department of Commerce - NOAA'};
    info.addTo(mymap);
```

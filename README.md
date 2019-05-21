# Hexagonal Density Map

### This project focuses on the creation of a hexagonal density map of U.S. Superfund sites via <a href="https://d3js.org/">D3</a> and <a href="https://leafletjs.com/">Leaflet</a>. Superfund data utilized for this map originated from the <a href="https://data.noaa.gov/dataset/dataset/superfund-sites">U.S. National Oceanic and Atmospheric Administration's Superfund Sites database</a> and map tiles by Carto via <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>.

#### Now, to go through the important portions of the code in the index file:

##### Styling

Map placeholder

```html
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
```html
>   .hexbin-hexagon 
>      stroke: #000;
>      stroke-width: 1px;
>    }
>   .hexbin-container:hover .hexbin-hexagon 
>  		transition: 200ms;
>  		stroke: limegreen;
>  		stroke-width: 5px;
>  		stroke-opacity: 1;
>  	 }
>  	.hexbin-tooltip 
>  		padding: 8px;
>  		border-radius: 4px;
>  		border: 1px solid black;
>  		background-color: white;
>  	 }
```

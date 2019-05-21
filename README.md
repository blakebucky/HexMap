# Hexagonal Density Map

### This project focuses on the creation of a hexagonal density map of U.S. Superfund sites via <a href="https://d3js.org/">D3</a> and <a href="https://leafletjs.com/">Leaflet</a>. Superfund data utilized for this map originated from the <a href="https://data.noaa.gov/dataset/dataset/superfund-sites">U.S. National Oceanic and Atmospheric Administration's Superfund Sites database</a> and map tiles by Carto via <a href="http://openstreetmap.org/copyright">OpenStreetMap</a>.

#### Now, to go through the important portions of the code in the index file:

##### Styling

Map placeholder

<code>
  <style> </br>
    html,</br>
    body, #map { width: 100%; height: 100%; margin: 0; background: #fff}</br>
    i {</br>
      width: 0.5px;</br>
       height: 16px;</br>
       float: right;</br>
       opacity: 0.7;</br>
    }</br>
  </style></br>
</code>

Setting Hexagons + Hover/Tooltips
>   .hexbin-hexagon {</br>
>      stroke: #000;</br>
>      stroke-width: 1px;</br>
>    }</br>
>   .hexbin-container:hover .hexbin-hexagon {</br>
>  		transition: 200ms;</br>
>  		stroke: limegreen;</br>
>  		stroke-width: 5px;</br>
>  		stroke-opacity: 1;</br>
>  	}</br>
>  	.hexbin-tooltip {</br>
>  		padding: 8px;</br>
>  		border-radius: 4px;</br>
>  		border: 1px solid black;</br>
>  		background-color: white;</br>
>  	}</br>

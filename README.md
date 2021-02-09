critter-world-map
=================

This is the zoomable map that was used in the Crittercism & Apteligent Geographic Performance pages.
Users can click to zoom down from world level to a country displaying first level province
boundaries. In the US an additional zoom level permits zooming into each state
displaying each county in the states.

Map data comes from a number of pre-prepared topojson files for the world,
each country and each US state. These have been built using the Makefile in the
natural-earth directory. Included shapefiles have been downloaded from
http://www.naturalearthdata.com/ and the us-atlas npm project.

The map is intended to be used as a choropleth, permitting each region at each
zoom level to be coloured based on quantized scale.

To view a demo, have a look here:

https://raw.githack.com/asparagino/critter-world-map/master/index.html

To test locally, you need to serve the index and json files from a local http server
to avoid CORS issues:

python -m SimpleHTTPServer 8000

Preparing Data
--------------

This map is intended for displaying global data collected with the geography files in mind.

* Data is keyed by 2 letter country codes at the world level, for example: **GB, BE, US**

* Within each country, first level administrative boundaries are keyed by ADM1 codes, 
corresponding to a primary administrative division of a country, such as a state in the
United States, for example: **USA-3521** represents California.

* Because US States are larger than many countries this is treated as a special case and states are further subdivided 
into counties. These are identified by US County FIPS codes, for example: **06075** identifies San Francisco.

For rapid ingestion or processing of discrete data points with latittude and longitude to group them into data to 
work with this map, you may find it useful to load the topojson geometry files into an rtree index on your server
and using it to calculate aggregate statistics.
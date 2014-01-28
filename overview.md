Jaanga Terrain Overview
=======================

Methods, tools, data and demos to create lively 3D cartography - faster and more easily than ever before 
## Concept

### Mission
Provide digital elevation data - in the form of heightmaps - for the entire globe at the highest resolution possible 
that is accessible as PNG files via HTTP from a few (currently four ) GitHub Pages-enabled repositories.

### Vision
Inspire entry and intermediate level programmers create wonderful new 3D cartography because the 3D data is so easy to access and the tools so engaging to play with.

<!--

## Concept
TMS in 3D
### Mission
Provide 3D terrain elevation data for the entire earth at 90 meter intervals - freely and easily accessible even to new and intermediate programmers.

###Vision
Develop demos and utilities that use the 3D data in clever ways for all the major coding languages.

-->

## The Issues/The Problems to be Solved

### Data Files are too huge
The data in question is the altitude above or below sea level at a specified interval of, say, every kilometer, 100 metres or even thirty meters for the entire surface of the earth. 

The common wisdom pr traditional thinking is that storing this data requires huge file sizes. For example, a data source used here, Jonathan de Ferranti's files with 3 second accuracy,
are supplied in 1,129 compressed ZIP files that occupy 15.1 gigabytes of disk space. Uncompressed this turns into 24,000 files and an additional 65 gigabytes of data.

This is not the sort data set that young or neophyte programmer are likely to be able to deal with. On top of that, the data is usually kept in obscure file types such as HGT or SHP files
that most people are not equipped to handle

It is our intention to to bring this deluge of data into a manageable container.

The original goal was to be able to store all the data in a single GitHub repository - which has a limit if about one gigabyte of files. 
We are not quite there yet, but we have managed t bring Mr de Ferranti's data down to 2.85 gigabytes spread over four repositories. 


### You need a PhD just to start
There are some sensational 3D cartography projects in existence. World Wind, Cesium and Google Earth come to mind. 
In terms of application QGIS and ArcGIS come to mind. But you are not going to sit down and bash out a new map in just a few hours.
These are professional tools for fully trained and committed engineers.

Entry level to us means that a beginner programmer can turn something out that is interesting with a couple of hundred lines of JavaScript and make it run on laptop.
No large data sets needed. All works in the browser. No plugin necessary. All FOSS. And fun to play with as well.

### No Filing System Standards
Everybody has there own way of doing things. NASA keeps its data differently that the US Forest Service who keep their data than Jonathan De Ferranti.

The 2D mapping world uses the TMS standard. The 3D world needs to follow suit.


## Strategies

Follow the TMS/Slippy Map system

* The folder structure in conjunction with the URL is used to index or catalog the files 
* PNG files are used to store the data

<!--


Live demos (using a JavaScript viewer):

<iframe src=3d-globe.html height=300 >
<a href=http://fgx.github.io/fgx-terrain/3d-globe.html><img src=images/3d-globe.png></a>
</iframe>

<iframe src=3d-flatland.html height=300 >
<a href=http://fgx.github.io/fgx-terrain/3d-flatland.html><img src=images/3d-flatland.png></a>
</iframe>
_3D Earth and flat map of California_

 Use your point device to pan, rotate and zoom. Once the projection issues are sorted out, these models will be overlaid with 2D maps. 
 Elevations are highly exaggerated. There is data missing before the international date line. The globe appears distorted at this scale because of the Mercator projection.

-->

## Introduction
Many online mapping services follow the [Slippy Map]( http://wiki.openstreetmap.org/wiki/Slippy_Map ) standard. 
Slippy Map is, in general, a term referring to modern web maps which let you zoom and pan around (the map slips around when you drag the mouse).

Online mapping services that support Slippy Map include Google Maps, Open Street Map, MapQuest, Stamen, ArcGIS and many others.

The basis of a Slippy Map is that the map image is built up of many little square images called "tiles". These are rendered and served from a "tile server".

It is a simple technology that provides an array of benefits and features that allow you to chop and mash map data in many ways. 
But the Slippy Map services generally miss out on a hugely important aspect of our world. The data is 2D but the world is 3D.

FGx Terrain supplies this much needed 3D data - while following the Slippy Map guidelines as closely as possible.

Slippy Map tiles follow a standard format: URL/zoom-level/X/Y.png. Zoom level 0 has one tile. Zoom level 1 has 2x2 tiles. Zoom level 2 has 4x4 tiles. 
All the way up to zoom level 18 which has 2^19 x 2^18 tiles. Every Slippy Map tile is 256 x 256 pixels.

Here is the most basic Slippy Map tile (from OSM):

![http://tile.openstreetmap.org/0/0/0.png]( http://tile.openstreetmap.org/0/0/0.png )

Link: [http://tile.openstreetmap.org/0/0/0.png]( http://tile.openstreetmap.org/0/0/0.png ) 

FGx Terrain supplies the 3D data by mimicking the standard, the URL and supplying a 'height map' for each Slippy Map tile from zoom level 0 to zoom level 18.

![http://jaanga.github.io/terrain/0/0/0.png]( http://jaanga.github.io/terrain/0/0/0.png ) 

Link: [http://jaanga.github.io/terrain/0/0/0.png]( http://jaanga.github.io/terrain/0/0/0.png ) 

The [bitmaps]( http://en.wikipedia.org/wiki/Bitmap ) (or images, [raster graphics]( http://en.wikipedia.org/wiki/Raster_graphics ) ) described here are of a special form.
Each pixel designates an altitude above or below or equal to a datum. Very often, these types of bitmaps are termed 'height maps'.

The current objective is to supply individual height maps for each Slippy Map tile up to zoom Level 7.

For tiles above level 7 there will be simple procedures that interpolate data from large (perhaps 2048 x 2048 pixels) height maps and produce the desired data at run time.
A preliminary version of the interpolator function can be viewed in the [FGx Plane Spotter]( https://github.com/fgx/fgx-plane-spotter/ ) app.

Sample of these procedure in a variety of languages such as written in Python, GO, or C will be made available.

The height data embedded in the images can be used for a variety of purposes. The use cases for this data include

* Building 3D Globes
* Building flat maps that have altitude
* Ascertaining the altitude of any airport or determining the rise and fall of a bicycle ride
* Assisting the calculation of the insolation (the amount of sunlight) on a building or area
* Assisting with land use planning
* Making geological features more apparent or visible



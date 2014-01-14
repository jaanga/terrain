Jaanga Terrain
==============

TMS in 3D

## Concept

### Mission
Provide digital elevation data for the entire globe at the highest resolution possible that is accessible via HTTP from a single GitHub Pages-enabled repository.

### Vision
Because the data is so easy to access and the tools so easy to play with, beginner and intermediate level programmers create a wonderful new 3D geography.

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

 Use your point device to pan, rotate and zoom. Once the projetion issues are sorted out, these models will be overlayed with 2D maps. 
 Elevations are highly exaggerated. There is data missing before the international date line. The Gobe appears distorted at this scale because of the Mercator projection.

## Concept
### Mission
Provide 3D terrain elevation data for the entire earth at 90 meter intervals - freely and easily accessible even to new and intermediate programmers.

###Vision
Develop demos and utilities that use the 3D data in clever ways for all the major coding languages.

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

Sample of these procedurs in a variety of languages such as written in Python, GO, or C will be made available.

The height data embedded in the images can be used for a variety of purposes. The use cases for this data include

* Building 3D Globes
* Building flat maps that have altitude
* Ascertaining the altitude of any airport or determining the rise and fall of a bicycle ride
* Assisting the calculation of the insolation (the amount of sunlight) on a building or area
* Assisting with land use planning
* Making geological features more apparent or visible
 


## Issues & Notes

The current Terrain height maps follow a different projection system than the one used by most Slippy Maps.  We are currently researching the best methods for reconciling the differences. 

This repo currently contains every folder and file required to display height maps for Slippy Map levels 0 to 7.

Currently the folders contain height maps only up to level 7 - After that there is a folder titled 7+ that has .


### Copyright and License
[FGx copyright notice and license]( https://github.com/fgx/fgx.github.io/blob/master/fgx-copyright-notice-and-license.md )

This repository is at an early and volatile stage. Not all licensing requirements may have been fully met let alone identified. It is the intension of the authors to play fair and all such requirements will either be met or the feature in question will turned off.

In preparing this data much use has been made of [GDAL]( http://gdal.org ) and [Image Magick]( http://imagemagick.org ). Thank you for the usefil tools.

The current source for the height maps for levels 0 to 4 is [CleanTOPO2]( http://www.shadedrelief.com/cleantopo2/index.html ). 
The license is: 'You are welcome to use the contents of this site for personal use.'
Thank you. 


## GDAL

There are extensive note on how the GDAL utiliies are used to build the heightmaps in the [Jaanga Terrain Wiki]( https://github.com/jaanga/terrain/wiki ).

<!--
There are a number of ways to install GDAL

Links on the GDAL site:

* http://trac.osgeo.org/gdal/wiki/DownloadingGdalBinaries

Two we have looked at:

* <http://trac.osgeo.org/gdal/wiki/DownloadingGdalBinaries>
* <http://fwtools.maptools.org/>


Our current favorite way is via oSGeo4W:

* [OSGeo4W]( http://trac.osgeo.org/osgeo4w )



This app allows you to install GDAL/OGR, QGIS, GRASS, Python and much more - perhaps too much. 
If you want a minimal installation, you can use the 'Express Install' and just selecy GDAL. 
And then run 'Advanced Install' and add the Python utilities - which includes gdl2tiles.py.

We could have learned a lot faster if we had found this page earlier:

<http://alastaira.wordpress.com/2011/07/11/maptiler-gdal2tiles-and-raster-resampling/>

Here is the command line we are using:

    gdal2tiles -e -n -p mercator -r bilinear -w none -z 0-7 input.tif output-folder/
	
Since we are using OSM format, we had to edit gdal2tile. We did so according to this link:

<http://gis.stackexchange.com/questions/63024/gdal2tiles-maptiles-from-bsb-kap-are-switched>

-->
	
	
## Change Log

2014-01-14 ~ Theo

* Data copied over from FGx Terrain and rebuilt. Will now be Jaanga Terrain, FGx Terrain wil be revived when there is navigational and aircraft data to be added.
* Data now based on Jonathan de Ferranti's 15 second data,


2013-12-31 ~ Theo

* Updated levels 0 to 4 with Mercator projection height maps.


2013-12-29 ~ Theo

* Added imges and demos
* Fresh data for zoom levels 0 to 4
* Updates to read me

2013-12-27 ~ Theo

* Read me updates

2013-12-26 ~ Theo

* Folders and files built and added
* files are all dummy images of the FGx Cap

 

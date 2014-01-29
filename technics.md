Jaanga Terrain Technics
=======================

This page covers some of the technical aspects that come into play in building the Terrain and Terrain Viewer repositories.

In the process of building Jaanga Terrain, we are coming across a lot of people's really neat and clever tricks. 
This section tries to catalog and report on the discoveries. And there will alwaybe be more to add and new tricks to discuss. 

Anyway this is a start... 

 
## Strategies: Play with Magic 

Highlights of the technical aspects include:

* Storing the elevation data in PNG bitmaps is highly effective
* Using and Abusing the TMS database
* GDAL utilities are black boxes of power
* The Canvas tag is your friend
* Crossing origins is good


## PNG files are used to store the data

We tried using ASCII JSON text files to store elevation data. There were many issues.
The file sizes soon becaume huge and transmission speed suffer. 
If all the data did not come in. the app is hosed.
There are too many numbers to be able to 'see' things.

We looked into using binary files, but these seem to require a whole lot of expertise and effert. 
The use of binary files did not seem to make hiles smaller or transmit faster.

The use of PNG files as heightmaps solves many problems and provides many benefits/

* Data is highly compressed without loss
* Files are transmitted and cached speedily and effortlessly
* Creating mash-ups with data from multiple servers is easy and permissible
* You can actually look at the file and see something
* The scope and range of tools to process PNG files is huge

 

## The TMS/Slippy Map system is used and abused

* The folder structure in conjunction with the URL is used to index or catalog the files 

## Introduction
Many online mapping services follow the [Slippy Map]( http://wiki.openstreetmap.org/wiki/Slippy_Map ) standard. 
Slippy Map is, in general, a term referring to modern web maps which let you zoom and pan around (the map slips around when you drag the mouse).

Online mapping services that support Slippy Map include Google Maps, Open Street Map, MapQuest, Stamen, ArcGIS and many others.

The basis of a Slippy Map is that the map image is built up of many little square images called "tiles". These are rendered and served from a "tile server".

It is a simple technology that provides an array of benefits and features that allow you to chop and mash map data in many ways. 
But the Slippy Map services generally miss out on a hugely important aspect of our world. The data is 2D but the world is 3D.

Jaanga Terrain supplies this much needed 3D data - while following the Slippy Map guidelines as closely as possible.

Slippy Map tiles follow a standard format: URL/zoom-level/X/Y.png. Zoom level 0 has one tile. Zoom level 1 has 2x2 tiles. Zoom level 2 has 4x4 tiles. 
All the way up to zoom level 18 which has 2^19 x 2^18 tiles. Every Slippy Map tile is 256 x 256 pixels.

Here is the most basic Slippy Map tile (from OSM):

![http://tile.openstreetmap.org/0/0/0.png]( http://tile.openstreetmap.org/0/0/0.png )

Link: [http://tile.openstreetmap.org/0/0/0.png]( http://tile.openstreetmap.org/0/0/0.png ) 

Jaanga Terrain supplies the 3D data by mimicking the standard, the URL and supplying a 'height map' for each Slippy Map tile from zoom level 0 to zoom level 18.

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




## GDAL

[Wikipedia]( http://en.wikipedia.org/wiki/GDAL ) says: 

> GDAL (Geospatial Data Abstraction Library) is a library for reading and writing raster geospatial data formats, and is released under the permissive X/MIT style free software license by the Open Source Geospatial Foundation. 

The various GDAL command line utilities have been instrumental in creating this repository.

## GDAL Install

There are a number of ways to install GDAL.

Links on the GDAL site:

* <http://trac.osgeo.org/gdal/wiki/DownloadingGdalBinaries>

Two we have looked at:

* <http://www.maptools.org/ms4w/>
* <http://fwtools.maptools.org/>

Our current favorite way is via oSGeo4W:

* [OSGeo4W]( http://trac.osgeo.org/osgeo4w )

This app allows you to install GDAL/OGR, QGIS, GRASS, Python and much more - perhaps too much. 
If you want a minimal installation, you can use the 'Express Install' and just selecy GDAL. 
And then run 'Advanced Install' and add the Python utilities - which includes gdl2tiles.py.

We could have learned a lot faster if we had found this page earlier:

<http://alastaira.wordpress.com/2011/07/11/maptiler-gdal2tiles-and-raster-resampling/>

## Typical GDAL Command Flow for Zoom Level Tiles 0 to 7

### The Project

Here is the overview of our current work method:

1. Take all the various data files and put them into one big height map
3. Divide the height map into the PNG tiles in all the zoom levels and at the same time warp the height map data from geodetic format to Mercator format

Are there better ways? Or things we can do to speed up the process. If so, please let us know.

### Data Source
Our data - the entire world with elevation data every 15 seconds - comes from the wonderful source provided by Jonathan de Ferranti:

<http://www.viewfinderpanoramas.org/Coverage%20map%20viewfinderpanoramas_org15.htm>

We downloaded all the files, unzipped them, and put them in a folder titled 'de15-tiffs'.

### Getting Info
The following command line segments are copied from the Windows DOS batch files we use.

We start by just seeing what's in the files and by finding the highest and lowest elevations. The command to use is `gdalinfo`:

    @rem Find highest and lowest points
    @rem Mount Everest = 8703
    gdalinfo -mm -stats -hist de15-tiffs\15-K.tif
    @rem Marianas Trench = -235
    gdalinfo -mm -stats -hist de15-tiffs\\15-L.tif

Using the `-mm -stats -hist` options adds a lot of time to the process. The first time just try `gdalinfo` without any options to see what the output looks like.


### Building a Vertices Index

Building a vertices index can really speed things up. We learned abour `gdalbuildvrt` through Bjorn Sandvik's blog _Themtic Mapping_ in his post '[Digital Terrain Modelling and Mapping]( http://blog.thematicmapping.org/2012/06/digital-terrain-modeling-and-mapping.html )'.

    @rem // buildvrt speeds things up a lot ~ multiple wildcards in single call OK
    @rem // can also use a list in a text file: gdalbuildvrt -input_file_list tile-list.txt de15-globe.vrt
    gdalbuildvrt -overwrite de15-globe.vrt de15-tiffs/*.tif

    @rem gdalinfo -mm -stats -hist de15-vrt/de15-globe.vrt

And once you have built the vertex index, you can see what's in it.


### Translate the Data to a Single PNG

We want to take all of Ferranti's data and put it in one file.

    gdal_translate --config GDAL_CACHEMAX 3000 -of PNG -ot Byte -scale -160 8703 0 256 de15-vrt/de15-globe.vrt de15-png-globe/de15-globe-0-0-0.png

Configuring a cache make things faster. See <http://wiki.orfeo-toolbox.org/index.php/Writing_large_images>. Also see Bjorn's post for details on setting the scale. You will note that we set it for the highest and lowest points on the earth.

By the way, we did try creating a large TIFF file, but the file becomes so huge that it is no fun at all to work with. We also looked at at using UInt16 instead of Byte to store the elevations but almost no app can deal with PNG UInt16 and when they can all you see is black so it's very difficult to do any visual error-checking.

### Creating the Tiles

We really hoped we could use Klokan's [MapTiler]( http://www.maptiler.com/ ) to create the tiles but our file is too big for the free version or normal human being priced version. So we used Klokan's student project, `gdal2tiles`:

    gdal2tiles --config GDAL_CACHEMAX 3000 -e -n -p mercator -r lanczos -s EPSG:4326 -w none -v -z 0-7 de15-png-globe/de15-globe-0-0-0.png de15-png-tms-dev/

Some points about the options

* Options are added in alphabetical order
* Again a large cache is used
* `-e` allows you to resume where you left off
* `-n` means don't create the extra files to build an app
* `-p` mercator` output in Mercator format
* `-r` lanczos' resample using a recommended technique - See Alistair A's post above.
* `-s` input is in geographic format
* `-v` let's us know what is going on verbosely 
* `z 0-7` builds the seven zoom levels
	
And - very important - since we are using OSM format, we had to edit `gdal2tile`. We did so according to this link:

<http://gis.stackexchange.com/questions/63024/gdal2tiles-maptiles-from-bsb-kap-are-switched>


### Typical GDAL Command Flow for Zoom Level Tiles 7+

Zoom level 7+ is the special level with heightmaps larger than the standard size 256 x 256 pixels. We cannot use `gdal2tiles` here because it only outputs tiles of 256 x 256. 

Here is our current work flow. Details to be supplied soon.

    @gdal_translate -projwin 47.8125 85.0511287798066 50.625 84.80247372433452 -q de15-vrt/de15-globe.vrt -scale -50 8000 0 255 temp.tif
    @gdalwarp --config GDAL_CACHEMAX 2000 -wm 2000 -q -s_srs EPSG:4326 -t_srs EPSG:3857 -r bilinear -overwrite temp.tif temp-mercator.tif
    gdal_translate -ot Byte -of PNG -outsize 100%% 100%% -q temp-mercator.tif de15-png-tms-try/7+/81/0.png



## The Canvas Tag is Your Friend

A significant and difficult aspect of this method of terrain data manipulation is the ability, the necessity to open a large 2D array of data, 
define a subset or slice of that array, then take that new array and resize the array arbitraily so that the new array has the correct dimensions 
and that every value in the array has been interpolated correctly.

If we are talking of doing this with standard numeric arrays, the matter is of suffiient complexity that you could probably write a PhD thesis or two on the topic.

Selecting the PNG file as the database allows you to compltely subvert this process.

The Canvas context [`drawImage` method]( http://www.w3schools.com/tags/canvas_drawimage.asp ) takes care of the entire proocess for you. And it is amazingly fast.







 



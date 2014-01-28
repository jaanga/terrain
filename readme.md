Jaanga Terrain Read Me
======================

![terrain/0/0/0.png]( 0/0/0.png )  
_terrain/0/0/0.png - the entire globe at zoom level 0_

This and the various other related Jaanga Terrain repositories only contain data. 
The terrain data - 3d elevation data for the entire globe in the form of PNG heightmaps - may be viewed as maps with a variety of viewers. 
Several viewer apps are available from the [Jaanga Terrain Viewer]( https://github.com/jaanga/terrain-viewer ) repository.

## Contents

An annotated table of contents for all the Terrain repositories on GitHub   

[Jaanga Terrain Contents]( http://jaanga.github.io/terrain/contents.html )

## Overview

The mission and vision for this work - as well as the issues that bring this project into being 

[Jaanga Terrain Overview]( http://jaanga.github.io/terrain/overview.html )


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

There are extensive note on how the GDAL utilities are used to build the heightmaps in the [Jaanga Terrain Wiki]( https://github.com/jaanga/terrain/wiki ).

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
If you want a minimal installation, you can use the 'Express Install' and just select GDAL. 
And then run 'Advanced Install' and add the Python utilities - which includes gdl2tiles.py.

We could have learned a lot faster if we had found this page earlier:

<http://alastaira.wordpress.com/2011/07/11/maptiler-gdal2tiles-and-raster-resampling/>

Here is the command line we are using:

    gdal2tiles -e -n -p mercator -r bilinear -w none -z 0-7 input.tif output-folder/
	
Since we are using OSM format, we had to edit gdal2tile. We did so according to this link:

<http://gis.stackexchange.com/questions/63024/gdal2tiles-maptiles-from-bsb-kap-are-switched>

-->
	
	
## Change Log

2014-01-26 ~ 

2014-01-22 ~ Theo

* de Farranti's 3 second data is online as PNG files
* There is beginning to be a fair description of the issues and the benefits


2014-01-14 ~ Theo

* Data copied over from FGx Terrain and rebuilt. Will now be Jaanga Terrain, FGx Terrain will be revived when there is navigational and aircraft data to be added.
* Data now based on Jonathan de Ferranti's 15 second data,


2013-12-31 ~ Theo

* Updated levels 0 to 4 with Mercator projection height maps.


2013-12-29 ~ Theo

* Added images and demos
* Fresh data for zoom levels 0 to 4
* Updates to read me

2013-12-27 ~ Theo

* Read me updates

2013-12-26 ~ Theo

* Folders and files built and added
* files are all dummy images of the FGx Cap

 

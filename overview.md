Jaanga Terrain Overview
=======================

Methods, tools, data and demos to create lively 3D cartography - faster and more easily than ever before 
## Concept

### Mission
Provide digital 3D elevation data - in the form of heightmaps - for the entire globe at the highest resolution possible 
that is freely and easily accessible as PNG files via HTTP from a few (currently four ) GitHub Pages-enabled repositories.

### Vision
Inspire entry and intermediate level programmers create wonderful new 3D cartography because the 3D data is so easy to access and the tools so engaging to play with.
Develop demos and utilities that use the 3D data in clever ways for all the major coding languages.

_2014-03-17 ~ The following is very much a work in progress_

## The Issues/The Problems to be Solved

### What is the best way to categorize, organize, and manage assets?

### Data Files are too huge: What are good ways for Managing and Storing 3D Elevation Data?
The data in question is the altitude above or below sea level at a specified interval of, say, every kilometer, 100 metres or even thirty meters for the entire surface of the earth. 

The common wisdom pr traditional thinking is that storing this data requires huge file sizes. For example, a data source used here, Jonathan de Ferranti's files with 3 second accuracy,
are supplied in 1,129 compressed ZIP files that occupy 15.1 gigabytes of disk space. Uncompressed this turns into 24,000 files and an additional 65 gigabytes of data.

This is not the sort data set that young or neophyte programmer are likely to be able to deal with. On top of that, the data is usually kept in obscure file types such as HGT or SHP files
that most people are not equipped to handle

It is our intention to to bring this deluge of data into a manageable container.

The original goal was to be able to store all the data in a single GitHub repository - which has a limit if about one gigabyte of files. 
We are not quite there yet, but we have managed t bring Mr de Ferranti's data down to 2.85 gigabytes spread over four repositories. 

### How do you use he heightmaps to create 3D Models.
Now you have shoulders that give nice bins for your data
- What 3D data are you going to put in those bins?
Good Shoulders Managing and Storing 3D Elevation Data:

Heightmaps
 
The Problem
There is a lot of data
If you need one data point for every tile at zoom level 18 
- then you need to manage 68,719,476,736 (68 trillion) items of data to cover the world
Any data format that is not fast, easy is likely to conflict with creating 3D maps.
Fun fact: TMS is good for any sort of data, not just maps.

The Barriers
Google provides an elevation service. If you are a Maps For business user you are allowed to acquire elevatiomns for 1,000,000 total locations per day.
So it would only take 68,000 days to acquire our data. And that data would be in ASCII JSON format.
One standard format is SDTS. See http://mcmcweb.er.usgs.gov/sdts/
Regarding SDTS, the Virtual Terrain Project says: \'it is a truly ugly, awful mess of a format\'
How about raw binary? Could this be the most efficient way.
http://www.ngdc.noaa.gov/cgi-bin/mgg/ff/nph-newform.pl/mgg/topo/customdatacd
This site offers 180 by 360 degree area (21600 rows X 43200 columns = 933,120,000 grid cells), and each data value will occupy 2 bytes. 
The uncompressed data file size will be 1,866,240,000 bytes.
Nearly 2 gigs of data here. Now we only need 73 more files like this to get to our one data point per leve; 18 tile
Oh and actually that tile is 150 meters per sided. We want to get to 30 meter resolition so we need 25 times that data.
Even the bimary data source we use - in HGT format - is \'only\' 65GB.
There is no way that you can build a realtime 3D TMS map with 65GB of normal binary data.

The implementation
Heightmap: 
Wikipedia: A raster image used to store values, such as surface elevation data, for display in 3D computer graphics.', '',
A heightmap can be used in 
* bump mapping to calculate where this 3D data would create shadow in a material
* displacement mapping to displace the actual geometric position of points over the textured surface
* terrain modeling where the heightmap is converted into a 3D mesh.
Your shoulders are on the third usage

Heightmap Benefits
Bitmaps travel fast.
Servers know how to send PNG files really well. 
So do ISPs and carriers.
And browsers know how to receive thme fast.
All of these services  understand, caching, deleting and transmitting bitmaps
Can do all this and garbage collection at run-time.
There\'s a lot of knowledge about bitmmaps - much more than other binary formats
lots of shoulders you can stand on
And, btw, bitmaps are an easy way to compress the s*** ot of data

BTW
Babylon has a great height map tutorial and buit-in functionality
https://github.com/BabylonJS/Babylon.js/wiki/16-Height-map

### No Filing System Standards. Where can you find a clean data Source?

Everybody has there own way of doing things. NASA keeps its data differently that the US Forest Service who keep their data than Jonathan De Ferranti.

The 2D mapping world uses the TMS standard. The 3D world needs to follow suit.

2D data is easy to get
Search Google for place + lan lon and you got the data
But no elevation or altitude data
It\'s as if we lived in a 2D world.

Where\'s the data?
Almost everything we know comes from a 2000 Shuttle mission
Now a mishmash of out of date stuff and broken links
Kind of weird: we know the lat lon of just about everywhere on earth,
 - but not it\'s elevation.
We are true flatlanders

The shoulders: Ferranti\'s site...


### You need a PhD just to start. What are some good tools?

There are some sensational 3D cartography projects in existence. World Wind, Cesium and Google Earth come to mind. 
In terms of application QGIS and ArcGIS come to mind. But you are not going to sit down and bash out a new map in just a few hours.
These are professional tools for fully trained and committed engineers.

Entry level to us means that a beginner programmer can turn something out that is interesting with a couple of hundred lines of JavaScript and make it run on laptop.
No large data sets needed. All works in the browser. No plugin necessary. All FOSS. And fun to play with as well.

Data procsseing shoulders: osGeo / GDAL

How do you get the data fron the Binary HGT files into PNG files?

GDAL: command-line driven. Fast. Not too difficult to learn
Crib sheet in Jaanga Terrain
Faster and more effective than Image Magick

My GDAL knowledge still at beginner level...


### It's still a lot of data: Where is a good place to keep the data?

GitHub Pages
Under utilized resource

So easy: just publish to branch with title \'gh-pages\'.
Nice limits: 1 GB per repo. Projects can have as many repos os needed
Publish any type of static data: HMTNL, CSS, JS, images, PDF etc
Use it as a starter Content Delivery Network

Jaanga Terrain data: 2.65 GB in 16K files: all on GitHub

BTW, GitHub has built-in readers for STL, CSV, and geoJSON files

### Working with raw binary files requires matrix multiplication - lots of it.. What are some tricks for doing this?

Working with bitmap files allow you to use the HTML Canvas element.

- getImageData and putImageData do the multiplications for you
- painlessly and very fast.
Canvas is a great shoulder to stand on.

### What are some good weys to create permalinks?

Use `Location.hash`.
It's an easy way to add and edit permalinks.

* Client-side oriented
* Real-time updating and clearing



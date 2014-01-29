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

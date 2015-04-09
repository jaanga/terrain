Dev Notes
===

2015-03-26 ~ Theo

* template-png-tms7-viewer-3d.html
	* code clean-up
	* Mostly fix altitudes




2015-03-23 ~ Theo

* node-jimp-topo30-to-png-tms7+.js
	* Does northern and southern hemispheres - about three minutes each

* template-png-tms7-viewer-3d.html
	* select map textures working with default and OSM textures

We are on a roll!

2015-03-22 ~ Theo

* Updates to template-png-tms7-viewer-3d.html
* Big code clean-up
* Basic Google/OSM overlay

2015-03-21 ~ Theo

* fixing template-tms7-htg-viewer-zip.html

* Add basic template-png-tms7-viewer-3d.html
	* Works nicely, but can use a cleanup

* Many failed attempts at getting lwip to handle large numbers of edits, but failed
* Luckily, came across jimp
* Jimp seems to do it all - fast and well.
* More on this tomorrow

Next

Lights
Levels 1-7
Google/OSM overlays << started
15 seconds / 3 seconds
topo > hgt > png tms7# << go
click on location map
placards
preferences
globe view
more gazetteers
cors iframe
permalinks
camera position
camera paths




2015-03-19 ~ Theo

* Slow day
* big file naming clean up
* Improved PNG TMS7+ Viewer 3D R1

* issue: node-srtm-to-tms-1-7-hgt-zip.js can only do one file at a time
	* Can't figure out how to get lwip to set pixels in batch mode

* But now can view PNG files turned into 3D without to many issues - happy accident whil mucking around with zip files
* so may leave zipped HGT path and go back to PNG heightmaps
* Bizarre turn of events

* Can use fs & node-png to read 900mb topo file and write out tms7+ png files
* But node-png cannot resize images
* So will have to use lwip or sharp for that operation 
* Everyday move ahead just a tiny bit and yet I keep thinking tomorrow it will be done but then something weird comes up.




2015-03-18 ~ Theo

* Build node-srtm-to-tms-1-7-hgt-zip.js
	* reads topo binary data
	* converts to ascii
	* converts to image data
	* resizes image data
	* converts to ascii
	* converts to binary
	* writes to zip file 
	* I don't believe it myself. Peeps like me can't do this stuff

* To be tested
	* Works at any zoom level
	* Processes the 1,000's of files nicely



2015-03-17 ~ Theo

* Reading zipped HGT files and turning into 3D
* Build node.js file that that reads to and creates the 16K+ TMS7+ files
	* Takes up about half the space as the original data 
* Build tms7-htg-viewer-zip.html
	* has gazetteer/location map


Coming next?

* San Francisco 1sec data
* map overlays
* placards
* TMS 1 - 7?


2015-03-14 ~ Theo

* Everything below seems to be done - except for placards
* New location map feature is awesome
* Parent/iframe integration going very smoothly


2015-03-11 ~ Theo

* tms7-htg-viewer-3d
* tms7-htg-viewer-bitmp
* Both progressing really well

* 3D needs
	* Calculate rowsPerTile
	* 2D web maps overlays
	* Better CSS

* Bitmap needs
	* Save to file?

* Both need
	* Location map
	* Gazetteer
	* Placards
	* Enter tile numbers
	* Update messages on changes

2015-03-10 ~ Theo

* R2 srtm-to-tms-hgt-node.js
	* Done!
	* Creates 8,300+ TMS7+ HGT files in 90 seconds

* SRTM to HGT TMS7+ Viewer R7
	* With new Hackette UI
	* loading files by file dialog
	* Simple NSEW navigation
	* Small & fun


2015-03-09 ~ Tho

* node parser:
	* Open file by name
	* handles start row, rows, start column, columns
	* save output
	* data seems to verify

* Started HGT Viewer R7
	* Oopen HTG file vie file dialog
	* Uses vA3C hacker sliding template

Should/could this be both canvas image viewer and 3D viewer?


2015-03-05 ~ Theo

* Wiping sand off my face
* I built a proof of concept demo that reads an HGT file, parses it and then saves it
* Should be abe to take the big SRTM files and breaks then down to TMS7+ size HGT files
	* Not as nice as PNG files. but a start
* Next hgt parser that allows you to select desired rows and columns
	* After that maybe straight ri TMS builder?


2015-03-02 ~ Theo

Now I have had sand kicked in my face.
It looks to me as if node-png or pngjs does not save an accurate representation of the HGT data.
Certain bytes appear to be wildly off. Many bytes off by a bit or two. Very strange.
 
What next?

1. Crop to TMS7+ size, save as binary then compress
	* learn to save as binary
2. See if Geoff can help with writing to PNG
	* Build small SRTM file test case for Geoff

 
2015-02-28 ~ Theo

* SRTM 16K new files created. takes about 5 minutes
	* GDAL has just had sand kicked in its face
	* Oops there is an issue with entire Southern Hemisphere but that should not take too long to find
	* The main thing is that a derp such as myself working on a laptop is able to process/mash-up 1.8GB of data and write to 16K files in a few minutes
	* Much of this is due to the V8 JavaScript compiler ( and its competition the other compilers ) and its ability to process web data quickly
		* When you bring this ability to the client-side desktop, it screams


2015-02-27 ~ Theo

* Reading SRTM plus data file into memory, creating multiple TMS7+ tiles in under 5 milliseconds each - with 150 lines of code
* Coming up next: create the 128 x 128 matrix of tiles!


2015-02-26 ~ Theo

* Can have node read split topo file
* amusing accident
* was having a lot of issues with node fs.read
	* could not set parameters to load portions of file I needed
	* Turned out I was using fileRead and I was always loading the entire 900mm each time - just about instantaneously
	* So why bother with portions when you can have the whole thing all at once
	* Makes code even more simple.
* Turns out lwip not very good at drawing multiple pixels
	* too many callback issues
* looked at pngjs - and its successor node-png
	* works fine


2015-02-25 ~ Theo

* Will work in c:temp/topo30 for now
	* means adding lwip there too
* topo30 file too big for node.
	* Explored many work arounds
	* Eventually: split file into two chunks
	* hope this works


2015-02-23 ~ Theo

Time to start this up again


2014-11-05 ~ Theo
Many nice things since last update.

It turns out, I could down load topo30 - a 1.8+ GB file and load bytes of it using JavaScript. All so easy, yet difficult to believe

Can access bytes 180000000 to 180000511 in 18 ms.

This should make everything much easier.

There are 43200 columns and 21600 rows.

Width/X/Lon
Need 128 TMS 7+ columns or 337.5 pixels per TMS. Perhaps can alternate 337 and 338 width columns

Height/Y/Lat
Needs to be calculated tile by tile.

Top lat is 85.0511.

Pixels from top = 120 * (90 - 85.0511) = 593.8679999999994 = 594
 
Equator at pixel 10800. 62 more to figure out. then flip for southern latitudes. ;-) 

All moving nicely today...


2014-05-06 ~ Theo
I have been bashing my head against cropping the big srtm30 plus files into smaller files. 
It's complicated and still a fail. Maybe I should try the de Ferranti files. 1 degree x 1 degree.
As and when I get that working, I can always come here and split the Scripps files into 1x1 files.


2014-04-29 ~ Theo

Several of the directories underneath have their own dev notes.
This is the beginning of the notes - and the process - that tries to tie all the work together.

An aside: It's interesting to watch the brain work. I feel that I am just a few hours away from accomplishing the first major goal of this project.
The goal is to translate the 33 SRTM30 Plus files into the 16,384 TMM7 heightmaps.
But it seems that instead of completing this much required and much sought for objective, the brain said: 'Today is a day where we tidy things up.'

I guess it's as if we know we are going to fight tomorrow and obtain a quick victory 
and then soon after march down Main Street in a victory parade.
So we want to do this with our shoes polished.
[And don't usually such certainties have issues?]

Anyway, there are so many files and scripts here that it is going to take some time to explain them all.
And it's looking like there are going to be quite a number of scripts that ended up on the cutting room floor / not required.
[So do these need explaining as well? Or should the be summarily sent off to some archive?]

Anyway: coming up there will be yet another folder: SRTM to TMS7.
Here we will try to go from the 33 SRTM files directly to TMS. 
The issue is that is you try to do sixteen thousand things dynamically, you end up with a free-for-all of management issues that slows things down.
Better to do one big file at a time.
And loading SRTM files and PNG files takes about the same amount of time.
We shall see...
 




Jaanga Terrain Further Considerations
=====================================


## Preface 2014-01-28
This is R1 for both data and code.

Jaanga Terrain holds the data and Jaanga Terrain Viewer has the apps.

It seems amazing that it is possible to compress over 265 gigabytes of binary data into just 2.85 gigabytes of PNG files. The question immediately arises as to what data has been lost, ignored or corrupted.

But then, now that it's been done, how could we do better? The GDAL utilities have a zillion possible parameters. Choosing the right ones may improve the quality of the data some or even a lot.

And the third question is the most fun: what apps or tools can we create that will help build the data faster, improve the quality and enable us to view the differences or trade-offs.

And then once that process is rolling nicely, it will be time to start adding the one second (data every 30 metres) data where that is available. With the current interpolation system it will be possible to have, say, 15 second data over much of the oceans and one second data in urban or geographically interesting areas only - and thus keep the total size of the data files down to a reasonable limit.


 
## Edge Conditions: Heightmaps

When you closely look at a page that display several tiles such as Terrain Viewer R5, you will notice a slight gap between the tiles.

It would be fairly easy to simply extend the maps just a few pixels further om each side and obliterate the error. In the other hand, the gap is a constant reminder that that there is a bug somewhere and the underlying cause of this discrepancy should be ascertained

In principle each mesh is built of a grid of 256 x 256 vertices and they are laid out so that the edge vertices of adjacent meshes should match perfectly. But as you can see they don't.

So where is the error?

Is it in the way the meshes are laid out? Is it in the way that the data is turned into a Mercator projection and transformed into a PNG file? Does the error have to do with tuning the binary data into the intermediate TIFF file? Or is there something we don't yet understand about Jonathan de Farranti's data.

We don't know yet. But the gaps are a constant reminder that there's something we need to investigate further.

 
## Edge Conditions: Tiles

The basic idea of a tile system is simple, elegant and workable: You take a large area, divide it into smaller areas and show one at a time.

Os course we had to go and complicate this process. It turns out that one tile just does not hold quite enough information nicely. Each tile is 256 x 256 pixels. Showing such a tile on a 2500 x 2000 monitor means that either the tile is tile or looks very crude.

For the time being we are showing four tiles at a time to make a square that is 1024 x 1024 units per side. It would be nice t0 have more but this really begins to slow down on most machines.

It would be great to have nine tiles at once. Then, for sure, the center of attention could be placed on the center tile. With four tiles, it gets a bit tricky. Very often the thing you are looking for is very near a corner. So, for example, you can have three quarters of a city not showing. Thus there is a routine that add the three tiles to the edges closest to the point in question.  

This works fine for zoom levels 2 to 7, but above that the interpolation routine kicks in and you know have a situation where you have a window(1) on a window(2) of the world. Well, sometimes window 1 wants to sit over two window 2s or when window 1 is over a corner it wants to sit over 4 window 2s.

An then there is the international dateline and you have to start all over again.

Little by little or actually edge by edge, these situations are being dealt with. Are they bugs? Not really. They are the system behaving exactly as it was told to behave. And so now we must give further more detailed instructions.

It's a fun little game of logic. So every time you see a tile that is flat or has not yet been updated from the previous view you can think we still have some more fun ahead of us.


2014-01-28 ~ This issue has been solved temporarily by building only a single 256 x 256 mesh

Note: this page should go to the Terrain Viewer repo...


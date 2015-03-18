![http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/cole-anstey-engine.png](http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/cole-anstey-engine.png)
This project is a 3d'ish volumetric editor for creating and editing voxel graphics.

The images below show v2 of the voxel editor supporting up to 128x128x128 blocks; which is written in c# and xna.
v1 used fixed 32x32x32 blocks which could be grouped together into larger blocks.
This became unmanageable hence the v2 rework to allow up to 128x128x128 trixels in increments of 8x8x8.

The terminology I use for the smallest unit of granularity is called a trixel (3 dimensional pixel); with 8x8x8 trixels make x1 mixel.
There can be up to 1..8x1..8x1..8 mixels in one voxel (128x128x128 trixels).

As you can see it's a bit like mspaint but you can zoom into the various cross sections using the mouse wheel.
You can also view the voxel from each of it's 6 faces.

The editor data is just z-ordered coloured pixels with the inclusion of the current voxel face direction.
The editor data is different from the data loaded into the actual game engine.

To use the editor data within the engine each cross section within each face direction is converted by...

a) creating a list of all unique colours in the current cross section.

b) grouping together all the pixels into the largest rectangular areas for each unique colour. I call these super pixels (see below). Each super pixel has a offset from an origin and a size. This step is the time comsuming bit.

Once this post processing is done and saved its pretty quick to load into an engine.

It seems to all work pretty quickly (once the engine data is processed) though at some future time I might find it doesn't scale and goes horribly wrong?

**Super pixels**

The following image shows a red colour being added to a initial black background and the algorithm grouping the pixels together into logical groups.

![http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/super-pixels.png](http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/super-pixels.png)

1st image contains x1 super pixel

2nd image contains x5 super pixels

3rd image contains x13 super pixels

**Voxel editor**

The yellow bars are trixels which have been changed.  When the voxel is saved these changes turn to green.  A feature like this is sometimes seen in text editors.
Each trixel face is edited independently of the overall three dimensional trixel;
so a trixel could have only one coloured face if desired.

![http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/Voxel-editor1.png](http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/Voxel-editor1.png)

**Voxel representation**

![http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/Voxel-editor2.png](http://3dish-volumetric-editor.googlecode.com/svn/trunk/images/Voxel-editor2.png)
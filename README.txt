ShapeFusion 0.5
http://shapefusion.sourceforge.net

An editor for Marathon II, Marathon Infinity and AlephOne scenarios

Copyright 2000-2008 Tito Dal Canton and Etienne Samson


What is ShapeFusion?
--------------------
ShapeFusion is a scenario editor for the AlephOne game engine, also
compatible with Bungie's original Marathon II and Marathon Infinity engines.
An AlephOne scenario is made of several files; ShapeFusion is devoted to
editing the "Shapes" file, which stores most of the scenario graphics and
animation data. It's *not* a tool for editing maps. In case you ever used
Bungie tools for editing Marathon scenarios, it's enough to say that
ShapeFusion is meant as a replacement for Anvil, or better for its Shapes
editor. Such a replacement is mainly needed because Anvil is proprietary,
non-free and Mac-only software, which makes it very difficult to use on
modern platforms. Thanks to Etienne Samson, since version 0.4 ShapeFusion
can open Sounds files too; the Sounds editor is in progress and I hope it will
reach the level of the Shapes counterpart soon.

As for the license, ShapeFusion is free software, released under the terms of
the GNU General Public License. For more information see the COPYING file
that comes with ShapeFusion.

Supported platforms
-------------------
ShapeFusion is being developed on Linux and continuously tested on Linux,
MacOS X and Windows. Thanks to wxWidgets it should compile and work on other
systems too, but I've never tried it. ShapeFusion could *in theory* compile
and work also on MacOS Classic, but I have no plans on this side. If you build
ShapeFusion on systems different from Linux, MacOS X and Windows, please let
me know (screenshots and binary builds are appreciated!).

Building
--------
You'll need wxWidgets (at least version 2.8.x) to compile ShapeFusion.

On Linux systems you can test the presence of wxWidgets by running the command
'wx-config --version'. If that command is available and gives you the right
version, everything should work; otherwise install wxWidgets following your
Linux distribution rules. To compile ShapeFusion, just run the following inside
the source directory:

  ./configure
  make

When compilation is complete, simply run the 'shapefusion'
executable (you can put it anywhere in your PATH). I finally suggest you place
the attached DefaultNames.txt file in the /usr/local/share/shapefusion
directory, so that collections and sounds will get Infinity-like names.

On MacOS X you should be able to use the provided Xcode project
(ShapeFusion.xcodeproj). You'll need both the MacOS X developer tools and
wxWidgets (which will take some time to build). Once in the ShapeFusion
Xcode project, before building you must change the WX_SRC_ROOT variable to
point to your wxWidgets source directory. Note that MacOS X binary builds are
released together with each source release: they should work out-of-the-box
without the need to install anything else. In case you're wondering why they
are so large in size, it is because they carry the whole wxWidgets library
together with ShapeFusion itself.

Overview of the Shapes editor window
------------------------------------
When you open a Shapes file, the window shows its collection slots on the left.
In standard Marathon Shapes there are always 32 of them; however, ShapeFusion
tries to be flexible and can open "extended" Shapes files with more collections,
like Damage Inc ones. Collection names are read from the DefaultNames.txt file
if it is available, otherwise they are set to simple numbers. Each collection
slot can be opened revealing two sub-slots, the 8 bit and true color versions.
They represent two independent versions of the same collection: the first will
be used if the game is played on low-color displays, the second is for modern
high-color displays (including the OpenGL mode in AlephOne). Each sub-slot can
finally be opened to reveal its real content: bitmaps, color tables, frames and
sequences. The contrast with Anvil is clear. Anvil tries to obfuscate some
aspects of the Shapes file organization, but I feel that this creates a lot of
confusion in the user. In my opinion, it makes more sense to treat Shapes files
as they really are: archives of collections. The ShapeFusion window tries to
reflect this idea.

Bitmaps, color tables and frames are displayed as lists of preview thumbnails.
Selecting one of them will pop up an edit panel for that item. Sequences are
listed by their name since they can't be easily represented with thumbnails;
however, selecting a sequence will pop up an edit panel like for other items.

The logic behind ShapeFusion is that each collection is made of four sets of
entities: color tables, bitmaps, frames and sequences. If you follow this
order, entities coming after reference entities coming before: a sequence
references a set of frames, a frame references a bitmap, a bitmap naturally
references a color table since it's indexed. So editing a sequence involves
picking frames from the collection frame set, and editing a frame involves
selecting a bitmap from the collection bitmap set. Get it? ;-) Of course you
don't have to follow this flow, especially if you are only adjusting some
settings.

The View menu contains display settings such as thumbnail size. Nothing here
affects what's inside the Shapes file.

You may edit the DefaultNames.txt file at your will to provide collection and
sound names that are more suited to your scenario. The syntax should be pretty
self-explanatory. Under Linux/Unix this file should go into
/usr/local/share/shapefusion; under MacOS X it should be embedded into the
application package (Contents/Resources); under Windows it should sit next to
the ShapeFusion executable.

Overview of the Sounds editor window
------------------------------------
TODO

Notes
-----
Please be careful when editing your scenario with ShapeFusion. We had no big
problems so far, but it's still under development and it may corrupt your
files, so be sure to keep backup copies. You should not use versions before
0.3, as they are affected by a bug regarding frames minimum light intensity
value. If you think your files got corrupted by ShapeFusion, please let us
know what happened.

Object indexes start from 0, not 1. So if you have 12 bitmaps, the first is
bitmap 0 (not 1) and the last is bitmap 11 (not 12).

Bitmaps are exported as 8-bit Windows bitmap (.bmp) files. They get the color
table that is currently used for viewing, as selected in the View menu.

When you import a bitmap, ShapeFusion tries to map its colors to the collection
color table as best as it can. Although the algorithm often yields good results,
you can help it a lot by converting the bitmap to indexed before (using
PhotoShop or Gimp, for example) so that it contains just colors belonging to
the collection color table.

In ShapeFusion, a frame can be referenced by many sequences. This may sound
strange at first, but in Shapes file format logic it's perfectly legal and I
think it makes sense too. However it can create a bit of confusion if you
forget it. Keep in mind that a famous Anvil bug is based on this very
confusion. But in Anvil it's a bug, in ShapeFusion it's a feature ;-)

If you open an "original" Shapes file (e.g. from Marathon II) and then save it
without touching anything, it won't probably have exactly the same size. In
other words, it won't be exactly the same file. However I've never been able
to tell the difference, apart from looking at the size. The original engines,
AlephOne and ShapeFusion itself seem to behave perfectly with both files. The
size mismatch has probably to do with data structure alignments: ShapeFusion
ignores alignments when writing files, it just packs structure after structure
and so produces generally smaller files.

Shapes files are known to rarely contain strange data, like negative sequence
ticks_per_frame. Maybe this comes from some broken Shapes editor, but it could
be just Anvil. ShapeFusion doesn't handle this invalid data very well, but I
plan to implement some consistency checks in the future.

Feedback
--------
You can send screenshots, bug reports and any comment to tito(at)dalcanton.it.
Better yet, you can join the ShapeFusion development mailing list
(see http://www.sourceforge.net/projects/shapefusion for details) and report
things there.

History
-------
ShapeFusion was born in 2000 as a MacOS Classic application. Working releases
were produced, but then I moved to other projects and the development ended
while ShapeFusion was still far from being a complete editor.

With the death of the Classic platform and the spread of AlephOne on different
operating systems I became more and more attracted by the idea of porting
ShapeFusion to other systems too. This couldn't be done easily with the
original MacOS code, so eventually I started to rewrite everything using the
portable wxWidgets toolkit. I also had the opportunity to rework the user
interface, since I never liked the Anvil approach that I was trying to follow
in the original ShapeFusion. Etienne joined the project at this stage.

The new editor is not yet complete, but it's a great improvement at least on
the technical side (stability, code organization, portability). Adding new
features and fixing existing ones will be much easier with respect to the old
version.

Changelog
---------
0.5
	Collection and sound names are now read from a simple external text file.
	First release supporting Windows officially.
	ShapeFusion now requires at least wxWidgets 2.8.x.
	Fixed a bug that prevented opening shapes files on Windows.
	Fixed a file I/O bug that prevented BMP exporting on Windows.
	Code cleanup and minor fixes.

0.4
	Switched to multidocument wxWidgets framework (major code rewrite).
	Implemented a preliminary Sounds editor.
	Implemented the color table editor.
	Improved the color quantization algorithm used when importing bitmaps.
	Bitmap masks can be exported to separate bmp files.
	Bitmaps are now exported to 8-bit bmp files.
	Lots of small changes and fixes.

0.3
	Improved functionality of the sequence editor.
	Implemented bitmap and frame deletion.
	Frame and sequence user interface cleanup.
	One can now edit frame scale factors.
	Fixed a serious bug regarding frames minimum light intensity value.
	Assorted changes and fixes.

0.2
	Work done on the color table section and on color table exporting features.
	Improved color reduction when importing RGB bitmaps.
	Implemented "Save all bitmaps".
	Implemented preliminary version of a true sequence editor.
	Implemented sequence deleting.
	Fixed sequence name charset issue that prevented some names from being displayed.
	BitmapBrowser and FrameBrowser speed optimizations.
	Assorted changes and fixes.

0.1
	First release of the new version using wxWidgets.


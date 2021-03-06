Description
===========

nnedi3 filter for VapourSynth.

This is a port of tritical's nnedi3 filter.


Usage
=====

::

   nnedi3.nnedi3(clip clip, int field[, bint dh=False, bint Y=True, bint U=True, bint V=True, int nsize=6, int nns=1, int qual=1, int etype=0, int pscrn=2, int opt=2, int fapprox=15])

Allowed values (ranges are inclusive):

- field: 0..3
- nsize: 0..6
- nns: 0..4
- qual: 1..2
- etype: 0..1
- pscrn: 0..4
- opt: 1..2
- fapprox: 0..15

::

   nnedi3.nnedi3_rpow2(clip clip, int rfactor[, int width=clip.width*rfactor, int height=clip.height*rfactor, bint correct_shift=1, int nsize=0, int nns=3, int qual=1, int etype=0, int pscrn=2, int opt=2, int fapprox=15])

Requires Firesledge's fmtconv plugin.

- rfactor

  Magnification factor. It must be a power of 2 between 2 and 1024.

- width

- height

  Dimensions of the output. These parameters only have an effect if *correct_shift* is True.
  If they are different from the default values, the image will be enlarged by *rfactor* and then scaled to the desired dimensions using fmtconv.

- correct_shift

  If set to True, the shift introduced by nnedi3 will be corrected using fmtconv's spline36 resizer. The same resizer will scale the image to *width*\ ×\ *height* pixels, if those parameters were provided.

  If the video is vertically subsampled, the vertical chroma shift will be corrected regardless of this parameter's value.


Compilation
===========

::

   ./autogen.sh
   ./configure
   make

objcopy from binutils is required.
yasm is currently not optional.

DLLs can be found in the "releases" section.


Things to do
============

- Support more than 8 bits/sample.
- The output is slightly different from the original filter's output (with opt=1). Some pixels are off by one.

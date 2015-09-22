## What is a Tilesheet?

**NOTE**: need to mention stuff about layers; can have an arbitrary # of layers.

**IMPORTANT**: You should be familiar with the concept of [tile engines](http://en.wikipedia.org/wiki/Tile_engine).

A tilesheet is an image that acts as source of graphical tiles for drawing a tilemap.

Hypatia stores tilesheets at `resources/tilesheets/` (relative to the script's working directory) in zip archives. Each tilesheet zip archive has two files: `tilesheet.png` and `tilesheet.ini`.

`tilesheet.png` is the source of graphical tiles.  `tilesheet.ini` describes `tilesheet.png` to Hypatia.

I highly recommend taking a look at `examples/resources/tilesheets` to get a general idea of building tilesheets for Hypatia.

## tilesheet.ini

Here is an example `tilesheet.ini`:

```ini
[meta]
tile_width=16
tile_height=16

[animations]
# water highlights
29=0.5,37
37=0.5,29

# torch
60=0.25,61
61=0.25,60

[animate_effect]
21=cycle

[flags]
# walls
0=impass_all
1=impass_all
2=impass_all
```

The ini file is broken up into four `[sections]`: `[meta]`, `[animations]`, `[animate_effect]`, and `[flags]`.

### [meta]

Here is how meta is used:


```ini
[meta]
tile_width=16
tile_height=16
```

The above tells Hypatia to interpret `tilesheet.png` as consisting of 16x16 tiles. Hypatia associates a number with each tile, this is how it assigns numbers:

```csv
0,1,2
3,4,5
6,7,8
```

These numbers are referenced when defining tile attributes in `tiles.ini`.

### [animations]

In our example we have:

```ini
[animations]
# water highlights
29=0.5,37
37=1.0,29
```

This tells Hypatia to make tile 29 into an animated tile by using tile \#29 as the first frame, and tile #37 as the second frame. The first frame will play for half a second, and the second frame will play for one second.

The syntax is:

`<tile id number>=<duration in seconds>,<tile id for the next frame>`.

### [animate_effect]

This section denotes which tiles to turn into an animation, and how. This is different from regular tile animations which are simply chained tiles. `[animate_effect]` defines ways of _automagically_ making animations using effects on a tile.

```
[animate_effect]
21=cycle
```

In the above example, tile \#21 will be turned into an animation which cycles its colors every frame.

### [flags]

Here's an example of making tiles 0 and 8 impassable/solid to players with the `impass_all` flag:

```ini
[flags]
# a description for tile 0
0=impass_all

# a description for tile 8
8=impass_all
```

As of writing this, `impass_all` is the only flag demonstrable in the `example/game.py` demo.

## Easy graphical editing

You should keep a GIMP/editable version of your tilemap handy, which has a layer beneath the layer of the tilesheet which is simply a grid/checkerboard whose cells are the tilesheet's tile size. Such as this for a tilesheet whose tile size is 16x16:

![16x16 grid](http://a.imageshack.us/img693/6449/nesscreen.png)

Here's an example of using it as described:

![Editing tilesheet in GIMP](http://i.imgur.com/mW8s02o.png)

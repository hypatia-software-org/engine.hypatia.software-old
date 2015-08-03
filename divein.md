---
title: Dive in!
---

Want to get started with Hypatia? Great! This page contains a wealth of information on how Hypatia works.

The included demo allows you to mess with all of it's code and resources, and as such is a great way to learn the basics of using Hypatia.

## Contents
{:.no_toc}

* Table of Contents
{:toc}

## Get started with the demo

* **Windows**:
  Download the [latest demo release]({{ site.hypatia_repo }}/releases/latest), extract it, and run `game.exe`.

* **Linux, Mac OS X, and other platforms:**
  1. Clone the [Hypatia Git repository]({{ site.hypatia_repo }}).
  2. From a terminal window, change directories into the cloned repository.
  3. Install Hypatia by running `pip install .`.
  4. Change directories into the `demo` directory.
  5. Run `python game.py`.

If you're still here, great! Read on to find out how a Hypatia game is created.

## Tilesheets

A tilesheet is an image that contains multiple graphical tiles for use in the game, much like a proof sheet in photography.

Hypatia stores tilesheets in `resources/tilesheets/`, relative to the game script file. The tilesheets are stored in ZIP archives, which contain two files: `tilesheet.png`, which is the tilesheet itself, and `tilesheet.ini`, which contains data about the tilesheet for Hypatia to use.

Here's an example `tilesheet.ini`:

```
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

This file is split up into 4 sections: `[meta]`, `[animations]`, `[animate_effect]`, and `[flags]`.

### [meta]

The meta section is used to tell Hypatia how to read the tilesheet. In this example, the tilesheet is made up of 16x16 pixel tiles, so `tile_width` and `tile_height` are set to 16.

Hypatia assigns a number to each tile based on this. A 3x3 tilesheet would have numbers assigned in the following pattern:

```
0 | 1 | 2
--+---+--
3 | 4 | 5
--+---+--
6 | 7 | 8
```

These numbers are referenced when creating the map, as you will see later.

### [animations]

The animations section is used to tell Hypatia how to render animated tiles, where each frame of the animation is a separate tile in the tilesheet.

In our example, we have tile 29 and tile 37 set as animations. However, you may notice that the line for tile 29 refers to 37, and the line for tile 37 refers to 29. This creates a looping animation.

The format of the animation lines is the following:

```
<tile id number>=<duration in seconds>,<tile id number for next frame>
```

Given our example, this means that the animated tile will have tile 29 for half a second, and then tile 37 for one second, before looping back to tile 29.

### [animate_effect]

This section tells Hypatia which tiles to turn into an animation. This is different from the animation section above, in that these animations only use one tile image. The animations are created by Hypatia automatically.

In our above example, tile 21 will be turned into an animation which cycles it's colors each frame.

### [flags]

This section denotes flags that are set on specific tiles. In our example, tiles 0, 1, and 2 have the `impass_all` flag set - which means that the player, and NPCs, can not pass through these tiles. Generally, you would set `impass_all` for walls, fauna, and other structures.

## Tilemaps

A tilemap is a file that tells Hypatia what tiles to draw on the screen. Each scene contains it's own tilemap.

A tilemap looks like this:

```
example
-1 -1 -1 00 00 00 00 -1 -1 -1
-1 00 00 00 00 00 00 -1 -1 -1
-1 00 00 00 00 00 00 00 00 -1
-1 -1 -1 00 00 00 00 00 00 00
-1 -1 00 00 01 01 01 01 01 -1
-1 -1 -1 00 01 00 00 00 01 -1
-1 -1 -1 00 00 00 00 00 01 -1
-1 -1 -1 00 01 00 00 00 01 -1
-1 -1 00 00 01 01 01 01 01 -1
-1 00 00 00 00 00 00 00 00 -1
```

Let's break this down. The first line of the tilemap is the name of the tilesheet to use when drawing this map. In this example, the name of the tilesheet is `example`.

After this, there is a whole bunch of numbers. These correspond to the numbers of the tiles in the specified tilesheet. In this example, we are using tiles 0 and 1. 

The tiles with the number -1 are empty tiles, nothing will be drawn in those positions.

## Scenes

A scene specifies all the data Hypatia needs to draw a map, including where the player starts, and data about NPCs.

Scenes are stored in ZIP archives in `resources/scenes/` and contain three files: `tilemap.txt`, `scene.ini`, and `npcs.ini`.

### scene.ini

The `scene.ini` file currently only defines the location that the player starts in when the map is loaded. It looks like this:

```
[general]
player_start_x=16
player_start_y=64
```

Note that the positions in this file are not tile positions, they are pixel coordinates. In our example, with 16x16 tiles, the player will start two tiles from the left and 5 tiles from the top (starting on the left-most tile would be `player_start_x=0`).

### npcs.ini

This file contains information about non-player characters in the map.

An example `npcs.ini` looks like this:

```
[jill]
walkabout=jill
position_x=180
position_y=180
say=Hello, world!
```

This creates an NPC named "jill" using the walkabout sprite "jill", who will say "Hello, world!" when the player interacts with them.

## Walkabout sprites

A character sprite consists of many actions. They can be standing still, walking, running, and facing in many different directions. Walkabout sprites let you create a sprite that will react properly to all these different states.

For example, a character walking in 4 directions (up, down, left, right) will need 4 GIFs (animated or not):

* `walk_north.gif`
* `walk_south.gif`
* `walk_east.gif`
* `walk_west.gif`

For the character standing still, you'll need an additional 4 GIFs - `stand_north.gif`, etc.

If you don't want to create that many GIFs, and don't care about additional animations, you can use one file named `only.gif`.

### Anchor points

Any GIF file used in the sprite requires a corresponding INI file - so `walk_north.gif` will have a corresponding `walk_north.ini`. This file contains the anchor points for the image.

Anchor points are (x, y) coordinates of where to pin objects to. In our example, our `walk_north.ini` may look like this:

```
[head_anchor]
0=0,2
1=1,3
2=2,2
```

`[head_anchor]` means that we are defining the anchor for the sprite's head. `0=0,2` means that the anchor point for the head in the zeroth frame is at pixel location (0, 2), and so on.

You should look at the walkabout sprites included with the Hypatia demo to see what they look like in action.

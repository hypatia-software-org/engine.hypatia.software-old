---
title: Create a game with Hypatia
---

## Contents
{:.no_toc}

* Table of Contents
{:toc}

## Welcome

Hello! This tutorial aims to guide you through the basics of creating a game with Hypatia.

We're assuming you already have Hypatia installed, if not, go over to the [Get Hypatia]({{ site.baseurl }}/get.html) page and follow the instructions for your operating system.

## Set up the directory layout

The base directory layout for a Hypatia game looks like this:

- `game.py`
- `resources/`
  - `tilesheets/`
  - `scenes/`
  - `walkabouts/`

The `resources/tilesheets/` directory contains tilesheets, which are images that contain multiple graphical tiles for the game - much like a proof sheet in photography.

The `resources/scenes/` directory contains scenes. Scenes contain a tilemap, which states what tiles to draw; NPC information; and information about the scene itself.

The `resources/walkabouts/` directory contains walkabout sprites - the sprites for the player, NPCs, and other game resources.

## Creating a tilesheet

A tilesheet is an image that contains graphical tiles that are used to draw the game.

A tilesheet looks like this:

![]({{ site.baseurl }}/assets/tilesheet.png)

This tilesheet is made up of 16x16 pixel tiles, but the number of pixels for each tile can vary from tilesheet to tilesheet, as long as they are consistent within the same tilesheet.

Each tilesheet has the tilesheet itself, `tilesheet.png`, and an associated INI file, `tilesheet.ini`. The `tilesheet.ini` file contains the following:

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

Let's break this down. This file is split up into 4 sections: `[meta]`, `[animations]`, `[animate_effect]`, and `[flags]`.

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
-1 -1 -1 11 11 11 11 -1 -1 -1
-1 11 11 11 11 11 11 -1 -1 -1
-1 11 11 11 11 11 11 11 11 -1
-1 -1 -1 11 11 11 11 11 11 11
-1 -1 11 11 01 01 01 01 01 -1
-1 -1 -1 11 01 11 11 11 01 -1
-1 -1 -1 11 00 11 11 11 01 -1
-1 -1 -1 11 01 11 11 11 01 -1
-1 -1 11 11 01 01 01 01 01 -1
-1 11 11 11 11 11 11 11 11 -1
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

Walkabout sprites are found in the `resources/walkabouts/` directory.

For example, a character walking in 4 directions (up, down, left, right) will need 4 GIFs (animated or not):

* `walk_north.gif`
* `walk_south.gif`
* `walk_east.gif`
* `walk_west.gif`

For the character standing still, you'll need an additional 4 GIFs - `stand_north.gif`, etc.

If you don't want to create that many GIFs, and don't care about additional animations, you can use one file named `only.gif`.

The `walk_south.gif` from the Hypatia demo looks like this:

![]({{ site.baseurl }}/assets/walkabout.gif)

### Anchor points

Any GIF file used in the sprite requires a corresponding INI file - so `walk_north.gif` will have a corresponding `walk_north.ini`. This file contains the anchor points for the image.

Anchor points are (x, y) coordinates of where to pin objects to. In our example, our `walk_south.ini` looks like this:

```
[head_anchor]
0=2,1
1=2,0
2=2,1
```

`[head_anchor]` means that we are defining the anchor for the sprite's head. `0=2,1` means that the anchor point for the head in the zeroth frame is at pixel location (2, 1), and so on.


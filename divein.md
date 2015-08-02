---
title: Dive in!
---

The included demo allows you to mess with all of it's code and resources, and as such is a great way to learn the basics of using Hypatia.

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

This section denotes flags that are set on specific tiles. In our example, tiles 0, 1, and 2 have the `impass_all` flag set - which means that the player, and NPCs, can not pass through these tiles. Generally, you'd set `impass_all` for walls, fauna, and other structures.

## Tilemaps

## Scenes

### Player

### NPCs

## Character sprites

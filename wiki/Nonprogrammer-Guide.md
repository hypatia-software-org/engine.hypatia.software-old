This guide shows you how to fiddle with the `example/game.py` demo game which is supplied with Hypatia to show off the engine's capabilities.

Everything you'll edit is in the `resources/` directory.

## Editing Graphics

The `resources/` directory contains two major graphical assets:

  * [[Walkabout-Sprites|Walkabout-Sprites]] in `resources/walkabouts/`, these are the player (inc. NPC) sprites/animations. Each individual sprite has their associated assets contained in a zip file.
  * [[Tilesheets|Tilesheets]] in `resources/tilesheets/`, these are used for drawing tilemaps for a scene.

## Editing Scene Data

Scenes are located in `resources/scenes/`. A scene is a zip file which contains the following files:

  * `tilemap.txt`
  * `npcs.ini`
  * `scene.ini`

### scene.ini

Currently the `scene.ini` file only defines the starting position of the human player, like so:

```
[general]
player_start_x=60
player_start_y=90
```

The above will start the scene with the player at pixel coordinates (60, 90).

### npcs.ini

You can create/place NPCs by editing the `npcs.ini` file. Here's an example:

```
[jill]
walkabout=debug
position_x=180
position_y=180
say=Hello, world!

[door]
walkabout=door
after_activate=destroy
position_x=132
position_y=164
```

The above will create two sprites. `jill` will be at position (180, 180), use the `debug` link:[[Walkabout-Sprites|Walkabout-Sprites]], and say "Hello, world!" if you talk to it. `door` will exist at position (132, 164), uses the `door` walkabout sprites, and after being interacted with, will cease to exist.

## What is a Walkabout sprite?

We're going to be talking about _animated gifs_ a lot.

Any character consists of many actions. Let's consider a sprite where you can either run or walk in four directions.

This means you'd need four GIF animations for each direction you walk in:

  * `walk_north.gif`
  * `walk_east.gif`
  * `walk_south.gif`
  * `walk_west.gif`

You'd also need four GIF animations for each direction you can run in:

  * `run_north.gif`
  * `run_east.gif`
  * `run_south.gif`
  * `run_west.gif`

The reality is, you can have sprites for any arbitrary direction or action, e.g., _fly_upward.gif_. Just be aware that as of the time of this document, the only methods that work out-of-box are:

  * `walk_north.gif`
  * `walk_east.gif`
  * `walk_south.gif`
  * `walk_west.gif`
  * `stand_north.gif`
  * `stand_east.gif`
  * `stand_south.gif`
  * `stand_west.gif`

### What if I just want to use one image?

You can just use one file named `only.gif`!

## What are AnchorPoints and AnchorGroups?

Any GIF animation sprite requires a corresponding `ini` file. This means `walk_north.gif` must have a corresponding `walk_north.ini`.

You define anchor points in an `ini` file, anchor points are (x, y) pixel coordinates of where to pin objects to. Remember: topmost and westmost are 0!

walk_north.ini:

```ini
[head_anchor]
0=0,2
1=1,3
2=2,2
```

`[head_anchor]` tells us we're defining anchors for a character's head, so stuff can be pinned to their head. `0=0,2` means the zeroth frame's head anchor is located at pixel coordinate `(0, 2)`. `1=1,3` means that frame 1's head anchor is located at `(1, 3)`. Frame 2's anchor is located at `(2, 2)`.

## Find out more!

Checkout the walkabouts included with Hypatia! They are two examples located in `resources/walkabouts/`, _hat_ and _debug_. Try messing around with them, and then running `example/game.py`.

At some point you'll probably want a good way to distribute recordings of gameplay.

I like to use `ffmpeg`, `convert`, and `gtk-recordmydesktop` in FreeBSD.

Trimming video from `[start seconds]` until `[duration seconds]` thereafter:

```
$ ffmpeg -i in.ogv -ss [start seconds] -t [duration seconds] -c:v copy -c:a copy out.ogv
```

### Converting to webm

.Note: why am I scaling?
```
$ ffmpeg -i in.ogv -codec:v libvpx-vp9 -quality good -cpu-used 0 -b:v 600k -maxrate 600k -bufsize 1200k -qmin 10 -qmax 42 -vf scale=-1:480 -threads 4 -codec:a vorbis -b:a 128k out.webm
```

### Converting to GIF

#### Limited color (probably not what you want)

This is by far the cleanest way of making animated GIFs from a low-color (like pixel art) recording.

```
$ ffmpeg -i 2015-06-28-trimmed.ogv -r 10 -vcodec png out-static-%03d.png
```

`%03d` means three-digit-leading-zeros. I used this so the hundreds of frames outputted would be sorted correctly. If you had _thousands_ of frames you'd use `%04d`.

You can also use `-r x` where x is the \# of frames per second you desire.

Now you have to convert those PNGs generated to frames of a GIF:

```
$ time convert -verbose +dither -layers Optimize -resize 600x600\> out-static*.png  GIF:- | gifsicle --colors 128 --delay=5 --loop --optimize=3 --multifile - > out12.gif
```

Finally cleanup all the PNGs made:

```
$ rm out-static*.png
```

#### Lots of color (probably not what you want)

Note: `-r 11` means to force 11 FPS; I like to add `-vf scale=320x240` to scale the GIF down to 320x240.
```
$ ffmpeg -i 2015-06-28-trimmed.ogv -r 11 -f image2pipe -vcodec ppm - | convert -loop 0 - gif:- | convert -layers Optimize - vers4_norgb.gif
```

You can trim down the size of the gif using a package called `gifsicle`, which is available on FreeBSD:

```
$ gifsicle -O3 in.gif -o out.gif
```

### references

  * http://superuser.com/questions/377343/cut-part-from-video-file-from-start-position-to-end-position-with-ffmpeg
  * https://medium.com/@ndorigatti/increasing-gif-export-quality-e2eb9efef845
  * https://gist.github.com/dergachev/4627207

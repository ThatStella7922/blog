---
layout: post
title:  "Reduce your audio quality"
date:   2024-01-24 00:00:00 -0400
categories: software audio
---

This is more just silly fun than anything useful, but I figured I'd make a small blog post about it. I was recently messing with ffmpeg trying to get a very low, almost unusable audio quality on some music just to see how it'd sound, and I ended up with something that I was happy with.

Here's a standard copy of Hadouk, better known as the hold music for Polycom-based IP phone systems (available on [files.thatstel.la](//files.thatstel.la/media/music/)):

<audio controls>
    <source src="http://files.thatstel.la/media/music/hadouk-polycom-hold-music.mp3" type="audio/mp3">
    <source src="https://files.thatstel.la/media/music/hadouk-polycom-hold-music.mp3" type="audio/mp3">
Your browser does not support the audio element.
</audio>

<br><br>

Now here's Hadouk after being run through the ffmpeg command I came up with:

<audio controls>
    <source src="http://files.thatstel.la/hidden/blog-support/20240124reduceyouraudioquality/hadouk-destroyed.mp3" type="audio/mp3">
    <source src="https://files.thatstel.la/hidden/blog-support/20240124reduceyouraudioquality/hadouk-destroyed.mp3" type="audio/mp3">
Your browser does not support the audio element.
</audio><br><br>

### Encoding your audio
The ffmpeg command I came up with involves the [Opus](https://opus-codec.org/) audio codec, which is a lossy codec commonly used in voice calls and other low latency, low bandwidth applications. When used properly, it delivers great sound quality with very minimal resource usage.

This however, is **not** proper usage of Opus and so it sounds downright awful (which is the point).

You'll need copy of ffmpeg (built with `--enable-libopus` which most are) and the following commands:

```shell
ffmpeg -i [INPUT] -ar 8000 -codec:a libopus -b:a 4k lowquality.opus
ffmpeg -i lowquality.opus lowquality.mp3
```

On that first command, replace `[INPUT]` with the path to the file you want encoded. Run them both and once they're done you'll have two files:
- `lowquality.opus` file
  - is the raw opus file which is often difficult to play
  - can be deleted if you don't need it
- `lowquality.mp3` file
  - is *much* easier to work with
  - is what you'll want to share

Enjoy your low quality audio!

---

If there's enough demand, I could create a little GUI utility written in Python and distributed as a single binary with PyInstaller that does this all for you.
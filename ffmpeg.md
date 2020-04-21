# Overview

This is a quick reference guide for some ffmpeg commands

## Take a frame from a movie

```
ffmpeg -i photo-instructions-zh_CN.webm -vf "select=eq(n\,34)" -vframes 1 zh_cn.png
```

* `-vframes`: frame to take

## Create a gif from a movie

```
ffmpeg -ss 3.0 -t 3.0 -i '2020-03-23 16-23-11.mkv' -f gif chinesekeyboard.gif
ffmpeg -i 20190312_130954_1.mp4 -vf scale=640:360 alienware.gif
ffmpeg -i 20190312_130954_1.mp4 -o alienware.gif
```

* `-ss`: skip to
* `-t`: time (duration)
* `-f`: format

## output to webm with alpha from mov

uses the VP9 codec

```
ffmpeg -i FACE_CN_Alpha_20203103.mov -c:v libvpx-vp9 -pix_fmt yuva420p photo-instructions-zh_CN.webm
```

* `-c:v`: library libvorbis VP9

## convert mp3 to wav

```
ffmpeg -i jobs_done.mp3 jobs_done.wav 
```

## Convert Image Sequence to webm

```
ffmpeg -r 30 -i images/zh_cn/%05d.png -b:v 2M overlay.webm 
ffmpeg -i images/zh_cn/%05d.png -r 30 -b:v 2M overlay.webm
```

* `-b:v`: set bitrate
* `-r`: set rate

## Capture Screen

```
ffmpeg -video_size 1920x1080 -framerate 25 -f x11grab -i :0.0 output.mp4
```

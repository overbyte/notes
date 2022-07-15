# Overview

This is a quick reference guide for some ffmpeg commands

## Take a frame from a movie

```
ffmpeg -i photo-instructions-zh_CN.webm -vf "select=eq(n\,34)" -vframes 1 zh_cn.png
```

* `-vframes`: frame to take

## Create a gif from a movie

```
# start at 1 sec, end at 3, scale to 640x320, output to 24fps gif
# simple
ffmpeg -i ~/Videos/Screencasts/Screencast\ from\ 12-07-22\ 15:31:20.webm -f gif -r 24 load-more-demo.gif
ffmpeg -i '2020-07-15 16-35-41.mkv' -ss 00:00:01 -to 00:00:03 -vf scale=640:320 -f gif -r 24 cheese.gif
# start at 3 seconds gif
ffmpeg -ss 3.0 -t 3.0 -i '2020-03-23 16-23-11.mkv' -f gif chinesekeyboard.gif
```

* `-ss`: skip to
* `-t`: time (duration)
* `-f`: format
* `-vf`: apply filters (`scale`)
* `-r`: framerate

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

## Remove Audio Track

```
ffmpeg -i input_file.mp4 -vcodec copy -an output_file.mp4
```
Source: https://unix.stackexchange.com/a/33864



## Scale

```
ffmpeg -i input.mp4 -vf scale=320:240,setsar=1:1 output.mp4
```
Note: cannot be used with `-vcodec copy`

Source: https://trac.ffmpeg.org/wiki/Scaling

## Trim

```
ffmpeg -i input.mp4 -ss 01:19:27 -to 02:18:51 -c:v copy -c:a copy output.mp4
```

Source: https://developers.google.com/vr/develop/unity/get-started-ios

## Fix input video dims not divisible by 2

```
ffmpeg -i 'Screencast from 15-07-22 11:17:20.webm' -vf "pad=ceil(iw/2)*2:ceil(ih/2)*2" cookielaw.mp4
```

Source: https://stackoverflow.com/a/20848224

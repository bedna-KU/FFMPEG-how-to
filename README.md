# FFMPEG

### Convert video to images (3frames per second)

ffmpeg -i video.mp4 -r 3 -f image2 image-%3d.jpeg

### Resize video (to 1600x1200)

ffmpeg -i input.ogv -vf scale=1600:1200 output.avi

### Video to half speed

ffmpeg -i input.mkv -filter:v "setpts=2*PTS" output.mkv

## Video - remove audio

ffmpeg -i video.mkv -c copy -an video_no_sound.mkv

## Video - add audio

ffmpeg -i video.mkv -i audio.mp3 -codec copy -shortest viseo_with_audio.mkv

## Video - cut (from position - length)

ffmpeg -ss 00:00:30 -i input.mp4 -t 00:00:05 -vcodec copy -acodec copy output.mp4

## Merge videos

ffmpeg -i "concat:input1.mp4|input2.mp4|input3.mp4" -c copy output.mp4

## Optimize video (to DVD quality)

ffmpeg -i input.mp4 -vcodec libx264 -crf 23 output.mp4

## Repair video (all frames as keyframe (keyint=1))

ffmpeg -i input.mp4 -vcodec libx264 -x264-params keyint=1:scenecut=0 -acodec copy output.mp4

## Web optimized video - MP4

### h264 video codec and aac audio codec because IE11 and earlier only support this combination

ffmpeg -i input.mov -vcodec h264 -acodec aac -strict -2 output.mp4

### For maximum compatibility

ffmpeg -an -i input.mov -vcodec libx264 -pix_fmt yuv420p -profile:v baseline -level 3 output.mp4

### VP8

ffmpeg -i input.mov -vcodec libvpx -qmin 0 -qmax 50 -crf 10 -b:v 1M -acodec libvorbis output.webm

### VP9

ffmpeg -i input.mov -vcodec libvpx-vp9 -b:v 1M -acodec libvorbis output.webm

### VP9 "Best Quality (Slowest) Recommended Settings"

ffmpeg -i <source> -c:v libvpx-vp9 -pass 1 -b:v 1000K -threads 1 -speed 4 \
  -tile-columns 0 -frame-parallel 0 -auto-alt-ref 1 -lag-in-frames 25 \
  -g 9999 -aq-mode 0 -an -f webm /dev/null


ffmpeg -i <source> -c:v libvpx-vp9 -pass 2 -b:v 1000K -threads 1 -speed 0 \
  -tile-columns 0 -frame-parallel 0 -auto-alt-ref 1 -lag-in-frames 25 \
  -g 9999 -aq-mode 0 -c:a libopus -b:a 64k -f webm out.webm

# ImageMagick

## Resize images (no aspect ratio)

convert '*.jpg[224x224!]' resized%03d.png

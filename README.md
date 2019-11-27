# FFMPEG-how-to
A few examples of how I use ffmpeg

### Convert video to images (3frames per second)

ffmpeg -i video.mp4 -r 3 -f image2 image-%3d.jpeg

### Resize video (to 1600x1200)

ffmpeg -i input.ogv -vf scale=1600:1200 output.avi

### Video to half speed

ffmpeg -i input.mkv -filter:v "setpts=2*PTS" output.mkv

## Video - remove audio

ffmpeg -i video.mkv -c copy -an video_no_sound.mkv

## Video - add audio

ffmpeg -i video.mkv -i audio.mp3 -codec copy -shortest output.mkv

## Video - cut (from position - length)

ffmpeg -ss 00:00:30 -i input.mp4 -t 00:00:05 -vcodec copy -acodec copy output.mp4

# ImageMagick

## Resize images (no aspect ratio)

convert '*.jpg[224x224!]' resized%03d.png

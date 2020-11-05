# ffmpeg-help

Common used command Lines:

1. publish RTMP
ffmpeg -re -stream_loop -1  -i <input_file> -acodec copy -vcodec copy -f flv rtmp://localhost/live/source1

2. Hardware transocde (with scale)
- ffmpeg -vsync 0 –hwaccel cuvid -c:v h264_cuvid -resize 1280x720 -i input.mp4 -c:a copy -c:v h264_nvenc -b:v 5M output.mp4
- ffmpeg -vsync 0 –hwaccel cuvid -c:v h264_cuvid -i input.mp4 \ -c:a copy –vf scale_npp=1280:720 -c:v h264_nvenc -b:v 5M output_720.mp4 \ -c:a copy -vf scale_npp=640:320 -c:v h264_nvenc -b:v 3M output_360.mp4

3. nginx-rtmp Transcode
ffmpeg -vsync 0 -c:v h264_cuvid -resize 1280x720 -i rtmp://localhost/live/${name} -c:v h264_nvenc -preset medium -profile:v baseline -b:v 1M -maxrate 1M -bufsize 2M -c:a aac -b:a 64k -f flv rtmp://localhost/preview/nanjing

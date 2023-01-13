### 1）将`1920*1080`压缩为`1440*1080`，FOV不变

ffmpeg -i 1920-1080.mp4 -vf scale=1440:1080 -y 1440-1080.mp4（input为1920*1080）

### 2）将`1920*1080`裁剪为`1440*1080`，FOV变小

ffmpeg -i 1920-1080.mp4 -vf crop=1440:1080 1440-1080.mp4

### 3）将多帧按序图像（1、2、3...）生成1920*1080 30fps视频

ffmpeg -i %d.png -vcodec libx264 -s 1920x1080 -r 30 -pix_fmt yuv420p out.mp4

### 4）将视频解析成多帧图像

ffmpeg -i out.mp4 img\%d.png

### 5）查看视频rotation信息

ffmpeg -i input.mp4（如果带有角度，则会显示rotation信息）
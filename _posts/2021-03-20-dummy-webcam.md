---
layout: post
title: "Dummy Webcam"
author: "Aman Roy"
author_link: "http://amanroy.me"
---

This hack will help in streaming a pre-recorded video like a webcam video in an ubuntu-based Linux distro.

## **Method**

**Step 1 :** Install `ffmpeg` and `v4l-utils`.
```shell
sudo apt install ffmpeg
sudo apt install v4l-utils
```

**Step 2 :** Install `v4l2loopback`.
```shell
git clone https://github.com/umlaeute/v4l2loopback.git
cd v4l2loopback
make
sudo make install
```

**<span style="color: red;">(Optional step: Only if step 2 fails)</span>** 
```shell
git clone https://github.com/umlaeute/v4l2loopback.git
cd v4l2loopback
sudo apt install dkms
sudo cp -R . /usr/src/v4l2loopback-1.1
sudo dkms add -m v4l2loopback -v 1.1
sudo dkms build -m v4l2loopback -v 1.1
sudo dkms install -m v4l2loopback -v 1.1
```

**Step 3 :** Record video from any application (**cheese** if you are using ubuntu) and save it on device.

**Step 4 :** Enlarge video by looping it `n` number of times. Let's say if I want a 60 minutes video and the recorded video is of 1 min. Looping the recorded video 60 times will make it enlarged as expected.
```shell
for i in {1..60}; do printf "file '%s'\n" input.webm >> list.txt; done
ffmpeg -f concat -i list.txt -c copy output.webm
```
**<span style="color: red;">Note: Change `{1..60}` as required. Also change the video file name to input.webm or anything else accordingly.</span>**

**Step 5 :** Start the virtual webcam. **(Do it every time when restarted)**
```shell
sudo modprobe v4l2loopback exclusive_caps=1
```

**Step 6 :** Know where the dummy webcam has been made.
```shell
v4l2-ctl --list-devices
```
**Example -**

![v4l2-ctl --list-devices output](/assets/images/Dummy_video/list_device.png)

<span style="color: red;">Take a note of the above path </span>

**Step 7 :** Stream
```shell
ffmpeg -re -i ~/Desktop/output.webm -map 0:v -f v4l2 /dev/video2
```
<span style="color: red;">Note: change `/dev/video` according to what you got from step 6.</span>


**Step 8 :** Change webcam setting and choose the dummy video option on any website or application.

![v4l2-ctl --list-devices output](/assets/images/Dummy_video/select_webcam.png)



Finish!
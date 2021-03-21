---
layout: post
title: "Dummy Webcam"
author: "Aman Roy"
author_link: "http://amanroy.me"
---

This method will help in streaming a pre-recorded video as a webcam video in an ubuntu-based Linux distro.

## **Procedure**

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

**<span style="color: red;">(Optional step: Only if above command fails)</span>** 
```shell
git clone https://github.com/umlaeute/v4l2loopback.git
cd v4l2loopback
sudo apt install dkms
sudo cp -R . /usr/src/v4l2loopback-1.1
sudo dkms add -m v4l2loopback -v 1.1
sudo dkms build -m v4l2loopback -v 1.1
sudo dkms install -m v4l2loopback -v 1.1
```

**Step 3 :** Record video from any application (**cheese** in ubuntu) and save it in home directory with the name `input.webm`.

**Step 4 :** Enlarge the recorded video from previous step to a **1 hour video** by looping it **60 times**.
```shell
for i in {1..60}; do printf "file '%s'\n" input.webm >> list.txt; done
ffmpeg -f concat -i list.txt -c copy output.webm
```
<span style="color: red;">Note: Change `{1..60}` as required.</span>

**Step 5 :** Start the virtual webcam. **(Do it every time when your system is restarted)**
```shell
sudo modprobe v4l2loopback exclusive_caps=1
```

**Step 6 :** Know the path where the newly created dummy webcam is present and make a note of it.
```shell
v4l2-ctl --list-devices
```
**Example -**

![v4l2-ctl --list-devices output](/assets/images/Dummy_video/list_device.png)

**Step 7 :** Stream
```shell
ffmpeg -re -i output.webm -map 0:v -f v4l2 /dev/video2
```
<span style="color: red;">Note: change `/dev/video2` according to what you got from step 6.</span>


**Step 8 :** Change webcam setting and choose the dummy video option on any website or application.

![v4l2-ctl --list-devices output](/assets/images/Dummy_video/select_webcam.png)



Fin.

---

#### **References**

<https://video.stackexchange.com/a/12906 />

<https://stackoverflow.com/a/46438765 />
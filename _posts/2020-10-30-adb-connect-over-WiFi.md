---
layout: post
title: "adb connect over WiFi"
author: "Aman Roy"
author_link: "http://amanroy.me"
---

While developing an Android app, many of the times you need to test your app on actual devices. For that, you need to connect your device through a wire. But I feel, _wired is weired_.

The Alternative to that can be going with a wireless solution.

#### **Temporary solution**

_**Step 1**_ : Connect your laptop/computer and smartphone on the same WiFi network.

_**Step 2**_ : Get your smartphone's local IP address. 
You can install <a href="https://play.google.com/store/apps/details?id=com.abhijay.ipaddress">this</a> for knowing your local IP address if you have no clue.

_**Step 3**_ : Connect your smartphone using USB cable.

_**Step 4**_ : Run these commands one after another.

```shell
adb tcpip 5000
adb connect YOUR_SMARTPHONE_S_IP_ADDRESS:5000
```

_**Step 5**_ : Disconnect your smartphone from USB cable.

For switching back to USB mode 
```shell
adb usb
```

#### **Permanent solution**

This solution is similar to the previous one. Here we are trying to do the same thing with the help of shell scripting.

Follow these steps once and you are done.

_**Step 1**_ : Create a file called `con` inside the home[`~`] directory. and paste these commands inside it.

```shell
#!/bin/bash

adb disconnect
adb tcpip 5000
sleep 3
adb connect $1:5000
```

_**Step 2**_ : Make the file executable. 

```shell
chmod a+x con
```

Now every time you boot your computer, you have to follow till 3<sup>rd</sup> step from the temporary solution section. Then run only one command.

```shell
./con YOUR_SMARTPHONE_S_IP_ADDRESS
```

After that, disconnect and enjoy!
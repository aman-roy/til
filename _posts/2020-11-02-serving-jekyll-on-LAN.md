---
layout: post
title: "Serving Jekyll on LAN"
author: "Aman Roy"
author_link: "http://amanroy.me"
---

Jekyll is a static site generator that I used for creating [my website](http://amanroy.me) as well for this [til](http://til.amanroy.me).

Most commonly, for making the Jekyll site available to localhost, the command used is - 

```shell
bundle exec jekyll serve
```

While serving it on the localhost, sometimes I felt the need of serving it to the whole network. Making it available to the whole network will allow the blogger/developer to test the website while it is made on smartphones also. 

For serving on the complete local area network, use `--host` flag along with the value `0.0.0.0`.

```shell
bundle exec jekyll serve --host=0.0.0.0
``` 

Now you can go to your system's internal IP address with the assigned port number _(default: 4000)_.


For finding out your system's internal IP address, use this command ([source](https://stackoverflow.com/a/26694162)) -

```shell
ip -4 addr | grep -oP '(?<=inet\s)\d+(\.\d+){3}'
```


> NOTE - It will list out all the IPv4 interfaces. Usually, the internal IP address starts with `192.168.X.X`.


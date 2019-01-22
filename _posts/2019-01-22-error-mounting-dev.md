---
title: Error Mounting /dev/sdbX at /media/
layout: post
---

Last night I taking back-up from my GNU/Linux pc with usb hard drive but I don't know how but I forgot to plug my pc because of this my pc was shut down. After that my usb hard drive gave me an error "Error Mounting /dev/sdbX at /media/". First, I was scared but after that I solved with this command:

```bash
sudo ntfsfix /dev/sdbX
```

X is which is used on your pc mine was this:

```bash
sudo ntfsfix /dev/sdb1 
```
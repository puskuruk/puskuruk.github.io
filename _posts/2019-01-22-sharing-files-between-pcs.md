---
title: Sharing Files With Basic HTTP Server
layout: post
---

Hi,

I couldn't post for a long time.I know but I will post more.

Last day I needed to share a film one linux pc to mac pc and we didn't had anything like usb drive, usb hdd etc. Then I run a simple HTTP server with python and this was useful, because of this I want to share.

1. First you need to open terminal. (Most of GNU/Linux systems you can open with ctrl+T)

2. After that you need to go to folder which you want to share
For example:
```bash
cd ˜/movies/alien
```

3. In the folder which you want to share you need to type this command
```bash
python -m SimpleHTTPServer
```

4. After you started your server you need to create a hotspot from your pc which you run your server.

5. You need to  connect this hotspot with other pc.

6. In your pc which run server you need to type this command to see your ip addres(If you know you can skip this step)
```bash
ip addr show
```

7. In your which you connected hotspot from your other pc you need to open a browser and in address bar you need to write
```
your.ip.address:port_which_is_running
```

For example:
```bash
192.168.2.1:8000
```

Tadaaa now you can see your file from another computer!
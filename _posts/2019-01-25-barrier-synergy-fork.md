---
layout: post
title: An easy way to manage multiple computers
---

Hi!

For now in my development setup I have 3 computers. One is my server(victor laptop, debian 9), one is my portable machine(x230, pop-os) and the other one is mac mini. I have one keyboard for mac mini and for other machines I needed to use their own keyboards. This could be very annoying sometimes. I knew there was a software which is synergy but this was very expensive for me but last day I saw barrier which is a free fork of synergy and I installed to my all machines after I read the source code . And now I can use my favorite keyboard which is the x230s own keyboard  for controlling everything.


([This](https://github.com/debauchee/barrier) is the link of their repository. They dont have .deb file for now but they have .dmg file for macOS and for other systems they have guides(For  [GNU/Linux](https://github.com/debauchee/barrier/wiki/Building-on-Linux) and for [windows](https://github.com/debauchee/barrier/wiki/Building-on-Windows). In documentation there was a missing part which is when you finished installation what will you make. These are the steps I made:

*First you need to open barrier software on your computer which will be server.

*After that you need to open barrier software in other computer to looking computer name.

*In your server computer you need to click configure interactively and configure server and write your other computers name with drag and drop the monitor icon.

*In your server computer you need to click start.

*You need to click Client and unclick the auto config in your other computers.

*After that you need to write your ip which can be seen on the server computer to other computers.

*Then click the start on the other computers.

Yeah! Thats it.


Hope you enjoy. :)
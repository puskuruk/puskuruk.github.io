---
layout: post
title: Linux Komut Satırından Nasıl Bootable Usb Oluştururum?
---

Önce tabikide bir iso dosyası indirmiş olmanız gerekiyor ve sonrasında:

```console
sudo dd bs=4M if=/indirdiğiniz/dosyanın/yeri of=/dev/sdX status=progress oflag=sync
```

sudo yazmamızın nedeni ==> yaptığımız işlemin super user izinleri gerektirmesi.

of=/dev/sdX yazdığım yere taktığınız diskin ismini girmeniz gerekiyor. Yanlış girerseniz girdiğiniz diskteki tüm dosyaları silecektir bu nedenle bu komutu girmeden önce 

```console
lsblk
````

komutunu girerek usb dosyanızın ismine bakabilirsiniz.
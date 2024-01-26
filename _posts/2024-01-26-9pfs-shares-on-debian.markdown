---
layout: post
title:  "9pfs shares on Debian"
date:   2024-01-26 00:00:00 -0400
categories: software debian
---

Eva and I like containerizing a lot of things on our home server that runs UNRAID, and things we selfhost go into VMs. It works out fine besides the somewhat high memory usage (512MB per VM), and file access can be a bit cumbersome for quick on-the-fly editing without using nano over SSH, as SFTP isn't really built with that kind of usage in mind.

Eva wanted a way to edit her site files from her desktop, so I immediately thought of **9pfs**.

QEMU's **9pfs** allows you to make virtual filesystem devices (`virtio-9p-device`) and expose them to guest VMs, which means that you can specify a directory on the host machine to be directly accessible by a guest OS. This works by using a pass-through file system by on the 9P network protocol for communication between the host and guest.

UNRAID itself also has nice integration for 9pfs, allowing you to expose any folder on your server to a guest VM, complete with mount tags. 

## Setting it up
To begin, you'll want to set up a 9pfs share on your host machine. This will differ between different platforms, so check their documentation. Make sure to keep note of the mount tag (how it will be identified to the guest).

### Adding the 9p modules to initramfs

Edit `/etc/initramfs-tools/modules` and add the following modules:
```
9p
9pnet
9pnet_virtio
```

Then run `sudo update-initramfs -u` and reboot.

### Mounting the 9p share

You can now mount this share manually with the following command, customizing the tag and mount point for your use:

```
mount -t 9p trans=virtio,version=9p2000.L,rw mymounttag /mnt/myfolder/
```

This isn't very useful though, since it will not be mounted after a reboot unless you run this command again.

### Adding the mount to fstab

Add this to the bottom of your fstab and the 9p share will be mounted automatically on boot. Make sure that your mount tag and mount path are set to what you need:

```
mymounttag /mnt/myfolder/ 9p trans=virtio,version=9p2000.L,msize=104857600,rw 0 0
```

### Done
After all that setup, you now have a shared folder working between a host and a guest machine.

Modify files from the guest, they show on the host. Modify files on the host, they show on the guest.
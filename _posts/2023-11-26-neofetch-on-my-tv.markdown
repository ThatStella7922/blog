---
layout: post
title:  "Neofetch on my TV"
date:   2023-11-26 00:00:00 -0400
categories: software modding
---

I recently got my LG C1 48" shipped to my new place here in Michigan after having to initially leave it behind and after getting it unboxed and running again, I wondered just what more I could do with it. I mentioned the possibility of rooting it via the RootMyTV to [my cat Eva](https://crystall1ne.dev), and from there both of us started researching what we could do.

RootMyTV is a very easy to use tool for LG TVs that involves you opening the web browser and clicking a button to root the TV and install the Homebrew Channel. It supports the majority of TVs on webOS 3.4 through 6.2 via various exploits.

Unfortunately, my LG C1 was made late enough that it shipped on webOS 6.3.2, meaning that RootMyTV is patched and will not work. Lucky for us though, the TV is vulnerable to another exploit.

## Enter `crashd`

`crashd` from my poking seems to be what keeps the user 'jailed' (i.e unrooted), but apparently LG left it vulnerable to patched `jail_app.conf` files. With this patched file, it allows for a telnet server running as root to be spawned by manipulation of one of the directories it has access to.

This is the basis of how this entire process works, and if you actually want to go through with rooting your TV, visit [this guide](https://gist.github.com/throwaway96/e811b0f7cc2a705a5a476a8dfa45e09f) to learn how to install the homebrew channel, exploit your TV, and finally root it to take complete control of the system. According to the guide, LG has started rolling out patches since October 30th 2023, so it's probably safe to assume that versions prior to that are vulnerable. See the comments on the guide for user discussion regarding compatibility.

## Exploring the shell

With the TV rooted and the Homebrew channel's SSH server running, we can pretty much do whatever we want, so Eva and I decided to run neofetch.

After sshing into the TV, we are dropped at a familiar environment: a minimal shell. From here I *had* to see what shell this thing was running, so I checked the shell variable:

```console
root@LGwebOSTV:~# echo $SHELL
/bin/sh
root@LGwebOSTV:~# 
```

This output means that it's probably running Busybox's `ash` shell, so I tried running busybox and sure enough:

```console
root@LGwebOSTV:~# busybox
BusyBox v1.29.3 (2022-12-14 03:07:49 UTC) multi-call binary.
[full output hidden because it's not relevant here]
```

I figured I'd try running neofetch on this shell, so I downloaded it by running the following command:

```bash
wget https://github.com/dylanaraps/neofetch/raw/master/neofetch && chmod +x neofetch
```

From there I could run it, and...

```console
root@LGwebOSTV:~# ./neofetch
./neofetch.sh: line 36: syntax error: bad substitution
root@LGwebOSTV:~# 
```

It will sadly fail, as neofetch explicitly requires actual `bash` due to it's use of bash-isms.

## Using `bash`

From here the obvious solution is to run actual `bash`, so that's exactly what I did. I ran `uname -m` to get the system architecture (which is aarch64 on my C1) and from there I decided to take the easy way and decided to grab a statically-linked build of bash from [this repository](https://github.com/robxu9/bash-static/releases/). Not having to worry about dependencies was why I went with this route.

After copying it to `root`'s home folder on the TV over SFTP and renaming it to just `bash`, you can now make it executable with `chmod +x bash`, and finally spawn a shell with the following command:

```bash
PS1="[\d \t \u@\h:\w ] $ " ./bash
```

After you run that, the prompt should change and as you can see below, the bash version variable now returns the version of bash we downloaded.

```console
root@LGwebOSTV:~# PS1="[\d \t \u@\h:\w ] $ " ./bash
[Sat Nov 25 23:12:01 root@LGwebOSTV:~ ] $ echo $BASH_VERSION
5.2.15(1)-release
[Sat Nov 25 23:12:08 root@LGwebOSTV:~ ] $ 
```

## Running neofetch

Now that we're in an actual `bash` shell, we can simply run the copy of neofetch downloaded earlier!

```console
[Sat Nov 25 23:14:20 root@LGwebOSTV:~ ] $ ./neofetch 
./neofetch: line 36: syntax error: bad substitution
[Sat Nov 25 23:14:24 root@LGwebOSTV:~ ] $ 
```

Or so I thought...

Turns out that Neofetch includes a [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) for the system's `bash` (which resolves to busybox!), so for this little experiment we can just remove it. You can either do this with `vi` (built into the TV) or modify it on a computer with another text editor and copy it over with SFTP.

Either way, once that's done, running neofetch now yields the following:

![](/images/2023-11-26-neofetch-on-my-tv/1.png)

A fun experiment to be sure, but not really useful. If you ever want to remove the files, just remove the `bash` binary and `neofetch`.
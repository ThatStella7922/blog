---
layout: post
title:  "HTTPS and HTTP site loading woes"
date:   2023-05-15 15:46:57 -0600
categories: update site
---

Recently, I've been messing around with an old computer I got my hands on for free. It packs the following specs:
```
CPU: Intel Celeron (Mendocino) @ 0.53GHz
└ CPU Cores: 1
iGPU: Intel 810
dGPU: None
Mobo: DFI CW35-S
RAM: 320MB (256MB+64MB PC100)
NIC1: BELKIN F5D7001 v1212 Wireless G Plus PCI card
NIC2: Siemens SpeedStream 1020 (maybe, it is RTL81xx-based)
SSD: SanDisk X110 120GB
OS: Windows XP Professional (i686)
Audio: idk and idc
```
I initially started off messing with Windows 2000, but after adding 256MB of RAM to it (for 320MB, up from 64MB) I realized that it's more useful to me running Windows XP SP3 for some older programs, so it's been running that for a couple days now. As I've been using it, loading stuff onto it (including an old version of Opera) and using various apps on it, I came to realize that I needed some things from my website(s), which is fine, I'll just put in a 10/100 Ethernet PCI card and get on the website! Unfortunately this led to some immediate problems.

## The HTTPS problem
These problems were major, because my sites couldn't load at all - the remote server would refuse to serve the page. This is because Windows XP & Opera 12 are so old that they don't support newer SSL/TLS versions (if at all), and all my sites enforce HTTPS for better security, as well as explicitly loading external resources via HTTPS. This meant that I had to make some changes to the websites to allow it to load via HTTP on older systems. Fixing it would be nice, as it complements some of the work I did earlier optimizing the CSS to not be completely broken on older browsers (I even "fixed" iOS 6 at some point.)

Since I've been rolling my [landing site](//thatstel.la) from scratch, I like to think that I have pretty good control over how it works, from structure to resource loading. This meant that I knew most of what I had to do as soon as I figured out the main problem.

## Fixing access
The first thing I tackled was my web hosting provider enforcing HTTPS for my site, which meant that it would refuse to serve anything over HTTP. This was an easy fix though, I logged into the control panel on my hosting provider and simply disabled HTTPS enforcement. This does reduce security slightly, but frankly the landing site, file store and this blog aren't mission critical anyway.

That was the easy part though, I still had to look at external resource loading. My landing site uses Twemoji and font-awesome as well as an external stylesheet, all of which are explitly loaded as HTTPS. Take these as an example:
```html
<link rel="stylesheet" href="https://files.thatstel.la/hidden/css/landing-styleshit.css">
```
```html
<script defer src="https://files.thatstel.la/hidden/fontawesome/js/regular.js"></script>
```
These both refer to the external resource explicitly with `https://`, and  [files.thatstel.la](//files.thatstel.la) only supports TLS 1.2 and 1.3. This means that if the browser only supports SSL 2/3 or TLS 1.0/1.1, the remote server will refuse to connect. I could switch to loading these resources insecurely, but that would at best create mixed content warnings and at worst block the resources from loading on newer browsers (due to security policy). Another solution could be using embedded JavaScript to detect if the page was loaded through HTTP or HTTPS, then load the resource using the respective protocol, but that would be overly complex and requires JS. There has to be a better solution!

For this particular use, it turns out there is one! Enter the **protocol-relative URL** (officially the [scheme-relative URL](https://url.spec.whatwg.org/#url-writing)). In practical use, this does exactly what I need. You use it by declaring your URL as such:
```html
//files.thatstel.la/hidden/css/landing-styleshit.css
```
In a proper HTML tag, it would look like this:
```html
<link rel="stylesheet" href="//files.thatstel.la/hidden/css/landing-styleshit.css">
```
Protocol-relative URLs are loaded according to the currently loaded page's protocol, so if the current page is loaded via HTTP, the resource will be loaded via HTTP, but if the current page is loaded via HTTPS, the resource will be loaded via HTTPS. This means that the page will now load external resources properly when loaded via HTTP, while not forcing them to load over HTTP when the page is loaded via HTTPS.

This fixed the website, but there's still one last thing to take care of.

```css
background-image: url('https://thatstel.la/landing-assets/IMG2931-LQ2.jpg');
```
I load an image in my stylesheet as a background and you can see that it's an explicit HTTPS URL. The rest of the stylesheet will load and apply just fine, but the image will fail to load. After a quick experiment, it turns out that protocol-relative URLs work just fine in stylesheets too! However, because I'm lazy, I didn't test how far back these work in stylesheets so I ended up doing the following:
```css
background-image: url('http://thatstel.la/landing-assets/IMG2931-LQ2.jpg');
background-image: url('//thatstel.la/landing-assets/IMG2931-LQ2.jpg');
```
First I try loading the image via HTTP, just as a fallback. Immediately after, I try loading it with the protocol-relative URL if the browser supports it. This takes care of loading the image over HTTPS when the page is loaded via HTTPS (at the cost of one mixed content warning with the HTTP attempt, but oh well!)

## Result

Here's an image of the site loaded in Firefox 12 on Windows 2000 (running in a modern web browser funnily enough, courtesy of [jslinux](https://bellard.org/jslinux/index.html)):
![Screenshot of my landing page loaded in Firefox 12 on Windows 2000](/images/2023-05-15-https-and-http-site-loading-woes/windows2000.png)
<br>
<br>
<br>
<br>
and for comparison, here's the site loaded in Edge 113 on macOS Ventura
![Screenshot of my landing page loaded in Edge 113 on macOS Ventura](/images/2023-05-15-https-and-http-site-loading-woes/macos.png)

It's not the prettiest thing on Windows 2000 but hey, it works! Compared to not loading at all, this is pretty good.
I'll also be enhancing non-HTTPS compatibility on the file store later, and I'll tweet out when I update this blog post about that.

As always, HTTPS access will continue to be available (and preferred), the HTTP compatibility is just for allowing older machines to visit the websites more easily.
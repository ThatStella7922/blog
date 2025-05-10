---
layout: post
title:  "OnePlus Pad Review"
date:   2025-05-10 14:00:00 -0600
categories: review oneplus
---

Recently I got my hands on a OnePlus Pad 1 as my very first modern Android tablet. I didn't get to keep it for long due to financial constraints, but I still had fun messing with it for a week. Since this is the first Android tablet I've actually used since the Galaxy Tab S2, I spent a while exploring it and what it could do. For the most part I’ll be comparing to the iPad Pro 12.9", since that’s the tablet I loved for the longest time until the days of modern iPadOS. I owned the 2018 A12X, 2020 A12Z and 2021 M1 variants so I have a good feel for their behavior, quirks and quality-of-life features.

## Hardware
We can start off with the basics: internals. The OnePlus Pad 1 uses a MediaTek Dimensity 9000, which is an octa-core part released in late 2021. It has three types of cores (prime, performance, efficiency) as well as LPDDR5X RAM and UFS 3.1 storage. You can get it with 8GB RAM + 128GB storage or 12GB RAM + 256GB storage, and I had the former model with 8GB + 128GB. 

Notably, the chip also packs the ARMv9-A architecture, support for hardware-accelerated AV1 decoding (as well VP9, H265 and H264), and is built on the 4nm node. For a 2021 chip originally designed for phones, these are great features and they make the Pad keep up with competition in late 2024/early 2025. As a comparison, it performs about as well as Apple’s A12X/Z in CPU performance, and is near A12X in GPU performance. It’s also surprisingly efficient and completely changed my view on MediaTek SoCs as I had only previously used their low-end stuff like the Helio A22, which is borderline ewaste. 

For wired connectivity, you have a USB Type-C 2.0 port supporting host mode (OTG), charging, and slave mode (normal computer connection). It unfortunately lacks DisplayPort Alt mode, so no native video output. There is also the OnePlus docking connector for accessories in addition to the magnetic charging dock for the OnePlus Stylo. More about where these are located in the General exterior features section below.

For wireless connectivity, Wi-Fi 802.11a/b/g/n/ac/ax (Wi-Fi 4, 5 and 6) are supported in 2.4GHz, 5GHz and 5.8GHz bands, however, 6GHz mode is not supported for 802.11ax (Wi-Fi 6). You also get Bluetooth 5.3.

Positioning is unfortunately limited to Wi-Fi and Bluetooth assisted triangulation via Google Fused Location. It does not have GPS hardware. (However, linking to a OnePlus phone can solve this, see the Ecosystem features section near the end of this post)

## Display
As for the display, it has a 2800x2000 11.6” (296 PPI) IPS LCD display with a 7:5 aspect ratio, variable refresh rate from 30Hz to 144Hz, 500 nit brightness and a 1400:1 contrast ratio. In my usage, the display on this thing is every bit as good as the LCDs we've come to know on iPad Pro in regards to brightness, color reproduction, and touch response. The lower pixel response times and refresh rate hitting up to 144Hz is very nice for the rhythm games I play and it also made scrolling in regular apps super smooth. You can also set the refresh rate per-app in OxygenOS 14 and later.

One sore point of the display is that it has no antireflective coating applied, only an oleophobic coating. The brightness is high enough to overcome the lack of an antireflective coating outdoors, but it’s not ideal regardless.

## Build
Basically it’s built like an iPad Pro.

Okay, something more useful: It has a full CNC-milled aluminum unibody with rounded sides and a flat top (for the pen to attach to), with the display glass smoothly fitting into the frame. The display itself has thin bezels with rounded corners and slightly beveled edges, it is not completely flat. It honestly looks quite modern, and I like that.

There were no creaks, pops, bending or anything of the sort in my time with the tablet. Build quality itself is easily on par with an iPad Pro and the tablet doesn’t feel hollow or cheap.

## General exterior features
One thing to note is that to hold this tablet upright you have to hold it with the USB-C port to the right, since it has the camera in a landscape orientation like an iPad 10.

There are two speakers on each side of the tablet for a total of four speakers.
As for the other features:
- Top
  - Volume buttons (on the left) 
  - Pen dock (on the right)
- Left
  - Nothing
- Right
  - USB-C port
- Bottom
  - OnePlus docking connector (for keyboard)

On the back of the tablet, OnePlus has put the camera and flash LED module in the middle of the tablet near the top.

![Image showing the OnePlus Pad 1 in its keyboard accessory, running crDroid](/images/2025-05-10-oneplus-pad-review/pad1.jpg)

## Cameras
The cameras on this tablet are not good, you can definitely tell that costs were cut here.

The rear camera is a 13MP sensor supporting up to 4K 30FPS video recording. It has no optical image stabilization and no optical zoom. As long as you keep it still, it takes soft-looking pictures with decent colors. It does have some software processing which cleans up what you see in the viewfinder, and it does process HDR to assist the dynamic range.

The front camera is an 8MP ultrawide sensor supporting to 1080P 30FPS video recording. It also lacks optical image stabilization, and the image quality is similar to what the rear camera gets you. Decent colors, but a very soft image with *some* help from software processing to improve dynamic range.

The front camera does have a feature called Limelight, which is basically like Apple’s Center Stage in that it will take advantage of the camera’s high FOV to crop the image and keep in frame for supported video apps.

Overall, for anything other than video calls or pictures/video in a pinch, you should look elsewhere. The cameras are simply passable.

## Audio
Audio is handled by a quad speaker setup with Dolby Atmos. Compared to iPad Pro speakers, they’re brighter and detail treble better at the cost of not having much emphasis on bass (even though the speaker drivers themselves are capable of it, via EQing). Loudness is no issue as they get louder than iPad Pro speakers while not distorting, which was very nice for spoken word. Even better for music, the bass stops hiding at higher volumes and it does sound good at the higher volumes.

Unfortunately, OnePlus opted to **not** put a 3.5mm headphone jack on the Pad so you can’t just plug any old audio device into it. You have to use USB-C headphones or dongles. As a bit of a consolation prize, it at least supports lossless audio over Bluetooth via LDAC and LHDC, which is more than what can be said for iOS devices.

## Biometrics and security
This tablet has only one option for biometric unlock, your face. It uses the front 8MP ultrawide camera to scan your face and it is NOT a proper IR + dot projector solution like Face ID or Windows Hello Face. However, it is fast and has a reasonable amount of security, enough to not be fooled by various pictures of my face on a phone, tablet, or printed on paper.

Aside from that, there is the normal complement of Android screen locks including six-digit PIN, custom length PIN up to 16 digits, full password (up to 16 characters) and a pattern. 

OnePlus also has a full set of security features in OxygenOS. First there is App Lock which requires a specific privacy passcode to open apps you choose to secure. Next, there’s Hide Apps which hides apps of your choice from across the system. You can get to them using a secret dialer code of your choice, or a shortcut on the homescreen. Both require authentication. Then, there is Private Safe. It is basically a folder with an additional layer of encryption (on top of Android's own file-based encryption) behind your privacy passcode that can store photos, videos, audio, or other files.

Finally, the most impressive one (in my opinion): System Cloner. It creates a separate, hidden, system that you can access by unlocking the tablet via a separate screen lock that is different from your regular one! Since it’s a full user profile, you can install whatever you want and sign into whatever you want and it will not affect your regular system.

As a technical aside, System Cloner takes advantage of Android’s user profiles infrastructure to create the second system, but the user created for System Cloner is **not** shown in the system user switcher or user list because it is not a normal user.

## Battery
Battery life is covered by a 36.99 Whr battery with 67W SuperVOOC fast charging. This battery provided battery life that I would say is as good or better than current iPads. I saw 6hr30m of screen-on time on the worst day which involved an hour of max brightness outdoors using Discord, Chrome and YouTube all at the same time, then about half an hour of playing Java Minecraft (via Pojav Glow Worm) with a 120FPS framerate cap at max brightness, and the rest was indoor YouTube with light games (like clash of clans or Arcaea with visual effects disabled) at 144hz wherever supported, Chrome browsing, chatting on Discord and a bit of Bluetooth music listening. 

The highest SoT I saw in my time with it was *almost* eleven hours, which consisted of indoor usage of YouTube, Chrome, Discord and lossless streaming in Apple Music. 

Standby time was very good, I saw 2% drain after 12hr (basically overnight) with all of my accounts signed in and normal amount of notifications coming in. I know some people post standby time with no apps installed and no accounts signed in so I made sure to measure after I had moved into the tablet.

For basic media and web consumption users, this tablet will offer very good runtime, probably over 15h of continuous video streaming and 10h or more for indoor web browsing since drains *very* slowly at lower brightnesses.

OxygenOS also has some battery health preserving features like smart charging (charging up to 80% overnight and charging the rest of the way in the morning) and a manual 80% charging limit toggle.

## Software and general usability
The Pad 1 runs OxygenOS 14 at the time of writing, and it was a pleasant experience. Android 14 in general has been the smoothest and most stable mobile OS I’ve used in a long time, and compared to the last Android tablet I used (Galaxy Tab S2) it is literally *worlds* apart. It genuinely felt as smooth as late iOS 13 versions (the good ones, not 13.1) on my A12X iPad Pro, and the number of features on offer is everything I expected out of Android. Emulators and apps that would require extremely annoying signing, sometimes entitlement setup, and JIT enablement on iOS just work with one tap here. File manager apps are plentiful, emulation is actually good, USB storage is well supported, Material You theming is awesome and well-supported by OxygenOS, icon packs exist at all, widgets are super useful and have been a thing for *years* which means that there are plenty of choices. Android is the single main reason that I enjoyed using this tablet as much as I did.

For pretty much any workload, this tablet will keep you happy. In terms of emulation, it is very capable of running PS2 games (via AetherSX2) like NFS Most Wanted and God of War, up to a 2x PS2 resolution in my experience. Another system I tried was GameCube via Dolphin, and The Legend Of Zelda Twilight princess is a solid experience with a very stable 30FPS at 1080p resolution.

For native Android games, I tried Zenless Zone Zero, Honkai Impact 3rd, Arcaea, Minecraft (bedrock), Minecraft (Java, via Pojav Glow Worm) and Clash of Clans. For Minecraft bedrock, Clash of Clans, Arcaea, and most other simple 2D/3D games I can very confidently say that the tablet will sustain a solid 144FPS with no issues. It's great.\
On the other hand, Minecraft Java is a bit of a mixed bag depending on what versions you want to run. Unmodded 1.20.1 ran pretty decently at fancy graphics 12 chunks, achieving from 85-100 FPS with some drops to 30-60 if you generated chunks super fast.\
As for Zenless Zone Zero and Honkai Impact 3rd, they also ran pretty well but I could tell Zenless struggled a little bit. Zenless I ran at native res with high graphics at 60FPS framerate cap, and in simpler areas it would achieve that just fine. In the most intense of battles though, it would drop to 40FPS which was noticeable, but not bothersome. Honkai Impact 3rd fared better, running at 60FPS with maxed out graphics pretty much constantly, even in complex battles in Superstring dimension.

In terms of productivity, it was great. Editing some documents in Google Docs, looking at spreadsheets in Sheets, reading PDFs, those all worked without issue as expected. Split screen mode + a popup window also worked well with no lag or stuttering to speak of if I used YouTube, Docs and Discord all at the same time.

Another thing I liked about OxygenOS in general is that it has a lot of iOS creature comforts that I’m used to as a former longtime iOS user. Little things like picking up an app on the home screen with one finger and using a second finger to quickly swipe across pages, or the ability to select multiple apps and drag those around all at once, are present. Another thing is “Global Search” which is basically Spotlight Search. It can integrate with supported apps to show results from inside them, and otherwise searches for apps, photos, files, contacts and the web.

Ergonomics of the tablet itself are basically identical to an iPad, palm rejection when holding it with two hands is fine as well.

## Software freedom
I will note that you can bootloader unlock this tablet extremely easily. There is no application process or registration required like Xiaomi. You just set up the tablet, enter developer settings and you can enable OEM Unlocking. Once you do that, you use the standard `fastboot flashing unlock` to unlock the bootloader.

Other than that, OxygenOS puts no limits on what you can do. If AOSP can do it, this can too. OxygenOS also comes with the normal suite of Google apps, with parts of the setup wizard including Google apps. However (and fortunately) you do not need an internet connection or account login to set this tablet up (unless Google FRP is active).

## Ecosystem functions
Ecosystem features are covered mainly by the OnePlus Multi-Screen Connect suite which let me link my OnePlus phone to the tablet. It offers always-on cell data sharing from the phone, positioning assistance from the phone, phone screen mirroring on the tablet, app casting to the tablet, sending and receiving texts (SMS/MMS/RCS), and making/receiving phone calls. Now, this isn’t just a hotspot and Bluetooth calls, it’s a bit special. It has the full Google Dialer and Google Messages apps preinstalled, but they only work once a phone is linked as this tablet does not have a SIM card slot or a cellular modem. What Multi-Screen Connect does, is it emulates a modem and SIM card, down to even emulating your phone number. This allows incoming calls to ring on the phone and tablet simultaneously, and you can make outgoing calls from the tablet as well. Apps will also see the correct phone number in the emulated SIM, for things like automated SMS authentication codes. Of course, the tablet doesn’t actually have your SIM. The linked phone still services all SMS/MMS/RCS and calls for the tablet over what I think is BLE.

That’s all cool, but the coolest part for me is the always-on cell data sharing. When a phone is linked, it shares its mobile data with the tablet as long as it can reach it. This isn’t like Apple’s Instant Hotspot where your iPad will show your phone in the network list and you can connect with one tap, no, this is always connected and always ready. OnePlus has even made it so that the tablet outright mirrors the phone’s cellular icons, so you will see your phone’s cellular strength and connection type in the status bar. Since none of this is serviced by Android’s built-in mobile hotspot infrastructure, it also happens to bypass cellular data hotspot speed limits imposed by carriers in the US. All of this I think is serviced over Wi-Fi Direct and Bluetooth.

The final cool feature of Multi-Screen Connect that legitimately makes this competitive for me is the fact that the tablet can make use of the phone's positioning hardware (including GPS) for location services in Android. For example, GPS navigation is a near perfect experience even though the tablet lacks GPS hardware.

## Overall thoughts
I think that OnePlus made a lower-cost iPad Pro with the benefits of Android, and they succeeded. It’s cheap while not compromising on the important parts of the user experience and still manages to deliver one of the best Android tablet experiences on the market, even holding its own against iPads. It earns a recommendation from me with how strong of a contender it is compared to something like the iPad 10 or iPad Air 4, especially at its current price of around 350 USD in the USA.\
It does just as much (if not more) than either of them can do, with a better screen to boot.

Compared to a lower end Samsung tablet, it may also prove to be a better choice depending on how much you need a high refresh rate display, large screen, and smooth software.

In the end, my only major dig against the tablet is its limited OS support. It launched on Android 13 with three years of Android updates and four years of Android security patches guaranteed, **and it has already had two Android updates** at the time of writing. This means that if you buy it right now, you will receive Android 16 as its final Android update, with one more year after that of security patches.

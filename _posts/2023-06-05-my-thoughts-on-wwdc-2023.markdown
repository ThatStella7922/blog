---
layout: post
title:  "My thoughts on WWDC 2023"
date:   2023-06-05 02:00:00 -0600
categories: update ios
---

Apple's WWDC 2023 online event just concluded and a *lot* of shit dropped, so let's get started! I'll be talking about things in the order of their appearance.

> "***This is going to be a historic day***." \- Tim Cook

# Hardware

## MacBook Air 15-inch
![Side view of the new MacBook Air 15-inch in the Starlight color](images/2023-06-05-my-thoughts-on-wwdc-2023/macbookair15.png)

The MacBook Air 15" is actually a quite small upgrade compared to the 13" model, and I think it's better to call it a variant rather than an update. You get a bigger screen (still IPS LCD, 224 PPI, P3 color gamut and 500 nits max brightness) and a bigger 66Whr battery that's good for up to 18 hours of media playback, or 15 hours of browsing in Safari.

A notable change from the 13" model is that the base model config gets the full M2 with the 8-core CPU and 10-core GPU, instead of starting at an 8-core CPU with an 8-core GPU.

The I/O is the same as the 13" model, the RAM and storage options are the same (base model packs a 256GB SSD w/8GB RAM) and even the color options are the same.

It's literally just an Air with a bigger screen. Price-wise, it's decent enough, starting at $1,299 USD. The 13" model got it's price dropped to $1,099 USD, and the old 13" M1 model stays in the lineup at the same $999 USD.


## Mac Studio
![Front view of Mac Studio](images/2023-06-05-my-thoughts-on-wwdc-2023/macstudio.png)

The Mac Studio. This is purely a spec-bump so I'll just list the changes quickly.

- Updated with M2 Max and M2 Ultra
  - Up to 96GB and 192GB of RAM respectively
- M2 Ultra has up to a 24-core CPU and 76-core GPU, with "up to 3.3x faster CPU performance" and "up to 6.1x faster GPU performance", but I think these figures are compared to M1 Max and not M1 Ultra.

Pricing is the same before, atleast at the base model.

## Mac Pro
![View of the top front of Mac Pro](images/2023-06-05-my-thoughts-on-wwdc-2023/macpro.png)

This is a big one, as every Mac Pro will now come with an M2 Ultra. This officially completes the transition to Apple Silicon, as the Mac Pro was the last machine still shipping with an Intel processor.

The machine now starts at $6,999 USD, and that gets you the following config:
- M2 Ultra with 24-core CPU and 60-core GPU
- 64GB RAM
- 1TB SSD

You can upgrade to the binned M2 Ultra which packs a 24-core CPU and 76-core GPU for an additional $1,000 USD, and you can of course further upgrade RAM and the SSD at the time of purchase.

On the rear of the machine, you now get six Thunderbolt 4 ports (each capable of DisplayPort 1.4+DSC) and two HDMI 2.1 ports (each capable of up to 8K60 with VRR, HDR and muktichannel audio) as well as the previous dual 10GbE ports, USB ports and 3.5mm audio jack.

For wireless, you get Wi-Fi 6E and Bluetooth 5.3, as is standard for modern high end Apple devices.

The internal layout is where things get interesting. 
![View of the internals of Mac Pro](images/2023-06-05-my-thoughts-on-wwdc-2023/macprointernals.png)

Starting off with the simple things, on the inside it has the same USB 3 port and dual SATA ports (with power connector) as the last generation.

Next up are the PCIe slots. This is the first Apple Silicon Mac with actual PCIe slots that you can slot any card into.
You get a PCIe x4 gen 3 slot which is occupied by Apple's I/O card from the factory, then four PCIe x8 gen 4 slots, and finally two PCIe x16 gen 4 slots.

The interesting thing here though is whether standard dedicated GPUs will work. I'm willing to bet that they *won't*, and here's why I think that: 

It's been known for a while that M1 and M2 don't support eGPUs in any way, but have you ever wondered *why* they don't work? It's not (just) because Apple wants you to buy a more expensive computer, as there's another major player in the computing space that had a similar problem.

### Ampere Altra[^1]
Let's take a quick look at the Ampere Altra, a server-focused processor which is currently available to users and developers in the form of a dev kit form:
![Top-down view of the Ampere Altra Dev Kit PCB with processor installed](images/2023-06-05-my-thoughts-on-wwdc-2023/amperealtradevkit.png)

This dev kit board packs an Ampere Altra processor with 80 ARMv8.2 arm64 cores at up to 2.6 GHz, and it supports standard M.2 NVMe SSDs and can run off-the-shelf GPUs like NVIDIA or AMD GPUs in OSes like Windows 11 arm64 or many flavors of Linux. How does it run off-the-shelf GPUs though?

The PCIe controller in Ampere Altra has a bug where it might generate incorrect memory addresses when recieving certain types of writes from the CPU, so to work around this they hand out Device-nGnRE[^2] maps instead of Normal
Non-cacheable[^3] maps for PCIe memory areas. With this change though, unaligned accesses to this device memory will fault, so a load/store emulator was added[^4] to emulate faulting addresses, keeping the system stable. You can read a tiny bit more about how such a fix would affect Macs at [this toot by marcan](https://social.treehouse.systems/@marcan/109296260480669304). With this, the Altra supports running standard GPUs in its various OSes, and as marcan says in the toot thread, "it's the first solution I've seen that would actually allow you to use eGPUs on Apple Silicon Macs, driver agnostic, without horrible app compatibility issues." Such a fix would work because the PCIe controller in Apple Silicon is broken in a similar manner!

Issue is though, such fixes aren't present in any shipping Asahi Linux kernel or in any public version of macOS. The latest macOS Sonoma *might* include fixes for use with the Mac Pro but it's very much a stretch and not likely to happen.

Other than that whole *ordeal*, the Mac Pro's PCIe slots should accept other devices perfectly fine, like sound cards, storage controllers, PCIe SSDs, video capture devices and network cards.

Overall, a strange machine but pros will certainly appreciate the performance and (compared to the Mac Studio) the fact that it has PCIe slots for non-GPU devices.

# Software

## iOS 17
iOS 17 is kinda underwhelming for me, but here's the stuff I found interesting:
- Find My Item Sharing (you can share AirTags presumably)
- Live Voicemail (shows what the caller is saying *before* you pick up)
- Audio message transcription
- Offline Maps

Live Voicemail will keep me from answering spam calls and audio message transcription is so nice because I'd *much* rather read a message instead of listening to it. Offline maps are excellent as a fallback for when you have no cell service, it means I can now delete Google Maps.

One final thing that I noticed Apple didn't talk about: sideloading.\
There was zero mention of it in the presentation, and you would think that they would have said something about it with the EU possibly requiring sideloading later this year.

Also, iOS 17 drops iPhone 8 and iPhone X, making the A12 the oldest supported SoC on iOS.

You can read more about iOS 17 at [Apple's website](https://www.apple.com/ios/ios-17-preview/).

## iPadOS 17
iPadOS 17 was also underwhelming, and again here's what I found cool:
- Lockscreen customization from iOS 16 makes its way to iPadOS (widgets and live activities too)
- Interactive Home Screen widgets (finally)

Not very much here but I just think that getting to feature parity with the iPhone is important.

This time, iPadOS 17 drops iPad 5th gen, iPad Pro 1st generation, iPad Air 2, and iPad mini 4, making the A10 the oldest supported SoC for iPadOS.

Again, you can find out more about iPadOS 17 at [Apple's site](https://www.apple.com/ipados/ipados-17-preview/).

## tvOS 17
FaceTime on your Apple TV sounds awesome and the new control center will definitely make switching audio devices and users a bit better. Some of the major behind the scenes stuff is Dolby Vision 8.1 support and support for third party VPN apps.

I didn't find a preview page for tvOS on Apple's site so to be safe let's just assume that only the Apple TV 4Ks continue to be supported (A10X, A12 and A15 versions)

## watchOS 10
Before anything else - 🦀🦀🦀 the Series 4 is still supported! 🦀🦀🦀

Anyway, follow-up medication reminders, offline map support and the new design philosphy for apps that apparently better uses then available screen real estate better all sound great. 

You can read the rest of the features [here](https://www.apple.com/watchos/watchos-preview/).

## macOS Sonoma (macOS 14)
macOS Sonoma, this one will be pretty nice. Here's what I immediately like:
- Widgets on Desktop
- iPhone Widgets on Mac (via Continuity)
- Game Mode (higher priority for games, lower latency for AirPods and controllers)
- Enhanced Screen Sharing (uses the media engine in ASi for smoother video, hopefully it won't be glorified VNC anymore)

They did mention some kind of game porting kit, and I would like to see how that works, as gaming on Mac currently relies on playing one of the two dozen native games or Wine + MoltenVK.

As for the hardware that was dropped, basically every 2017 Mac except for the iMac Pro. One notable machine that was dropped is the 12" MacBook Retina, the last of its kind.

Full feature list [here](https://www.apple.com/macos/sonoma-preview/) of course.

## All OSes
This is just the stuff I think will make the greatest difference for me, across all the new OSes.
- Better autocorrect
- Message search filters
- Better AirPods switching

# Conclusion
This WWDC was overall good with new powerful hardware (M2 Ultra looks insane) and decent enough software features, but there is one thing that I didn't mention previously.

## Apple Vision Pro
![Marketing image for Vision Pro showing a man viewing content in virtual space, using the Vision Pro device](images/2023-06-05-my-thoughts-on-wwdc-2023/realitypro1.png)
I mean this thing just looks insane. look at it.

![Marketing image for Vision Pro showing a woman viewing a movie on a huge screen in virtual space, using the Vision Pro device](images/2023-06-05-my-thoughts-on-wwdc-2023/realitypro2.png)
From the UI elements we saw in WWDC, this thing looks *polished*, and also iOS-based.

The design is also one of the most interesting I've ever seen, especially the front glass piece. Getting a piece of glass curved and shaped like that must be *expensive*, and it also has that signature purplish sheen to it which is a telltale sign that it has some sort of coating on it to help keep it clean. I wouldn't be surprised if that one piece of glass (because it is one piece) is super expensive to make.

![An image showing the UI elements of a visionOS app](images/2023-06-05-my-thoughts-on-wwdc-2023/visionos1.png)
visionOS is also super interesting in that it looks *specifically* geared towards augmenting your surroundings, not replacing them like other VR/AR solutions. I got real HoloLens vibes from it. Also the blurs look phenomenal, they got a real Microsoft Fluent design type of look to them, with all the frosted-looking blurs. I personally love how it looks.

Since it's iOS-based, Vision Pro will be able to run iOS apps on launch day apparently, and you can bet that once it releases, I'm going to try to get my hands on one and play either Arcaea or osu! on it.

The device runs an M2 for processing and rendering, and the brand new R1 seems to be relegated to processing sensor data, which is probably a good thing because of just how many sensors there are. There's eye tracking, hand tracking, LiDAR and TrueDepth cameras for understanding of you and your surroundings in 3D space, and all kinds of other sensors presumably buried in there for tracking all sorts of things.

All of this fancy design, computing and sensor stuff comes at a price, and Vision Pro certainly does, starting at $3,499. Very expensive but if the technologies it offers are as polished and as high end as Apple says they are, it might not be a bad deal.

It remains to be seen how well all this works, but first impressions are great and personally, I can't wait to try it.

[^1]: This whole Ampere Altra section is based off information I've gathered by talking to people who are well versed in working with Ampere Altra and PCIe in general, as well as reading loads of documentation. I think I've managed to get it all right, but if there's something I got wrong, *please* correct me. It'd help me learn and ensures accurate info for others who may read this! You can contact me at [thatstel.la](//thatstel.la)
[^2]: https://github.com/Tencent/TencentOS-kernel/commit/f454797b673c06c0eb1b77be20d8a475ad2fbf6f for commit info. For more info on nGnRE-type Device memory, see https://developer.arm.com/documentation/den0024/a/Memory-Ordering/Memory-types/Device-memory
[^3]: What are Normal memory and Device memory? See https://developer.arm.com/documentation/102376/0100/Normal-memory and https://developer.arm.com/documentation/102376/0200/Device-memory.
[^4]: https://github.com/Tencent/TencentOS-kernel/commit/adb335972fcb7a6b59bb8034498b1ffddfb37c97
---
layout: post
title:  "A closer look at iPhone diagnostics mode"
date:   2023-05-21 15:46:57 -0600
categories: update ios
---

**For this post, do note that I haven’t done much of any actual research and basing this off my experience with and knowledge about iOS devices and apple repair.**

I’ve always wondered about diagnostics mode on iOS devices, and it started years ago when I typed `diags://` into the address bar on my 5th gen iPod touch running iOS 9. If I’m remembering correctly, this URL scheme was associated with a Diagnostics app that was hidden from springboard (Home Screen) and it would basically just show a message asking you to visit Apple’s support site for assistance.

This app-based diagnostics mode appears to be the primary diagnostics solution for hardware scans, and pairing of components like Touch ID looks to have been done by booting the phone from a special environment that only Apple has access to.

I’m not 100% sure about this (and details are hard to come by) but it seems like this changed with the iPhone 12. On this phone and all subsequent models, you can boot into a separate diagnostics mode by shutting it down, then plugging in a Lightning cable while pressing and holding both volume buttons. 

This diagnostics mode replaces the old “special environment” and is one that end-users can easily boot into, and it’s actually used in things like Self Service Repair if you need to do “System Configuration” for newly installed parts. 

This diagnostics mode looks to still be iOS, but there’s some things about it that are just..*off*.

Here’s everything I’ve noticed so far:
* On notched devices, the spacing for the status bar icons will be uneven or generally incorrect - this is the strangest to me
* On devices with a Dynamic Island, the cellular icons will be completely hidden, leaving only the battery icon, so no signal strength indicator or SOS/satellite badges, but if you connect to Wi-Fi, the icon will appear in the status bar as normal
* High refresh rates are supported, scrolling will be smooth at 120hz so I assume this means that there is GPU acceleration in diagnostics mode
* You can’t connect to a cellular network so no data, calls or texts
* You don’t have control of the currently running app, gesture navigation is completely disabled
* Access to Control Center is disallowed
* On devices with a Dynamic Island, tapping the island does nothing whereas in iOS it reacts slightly to your touch
* Preferences from the normal iOS installation don’t carry over, such as keyboard haptics, light/dark appearance, text size, accessibility features, etc
* Known Wi-Fi networks from the normal iOS installation don’t carry over
* Userdata as a whole from the normal iOS installation seems to be completely ignored, you don’t need to authenticate with your passcode or Apple ID to use diagnostics mode
* Diagnostics mode doesn’t save any data, like Wi-Fi networks you connect to 
* The entire diagnostics mode environment seems to be silent outside of actual hardware tests that use the speakers, you’ll never hear a keyboard click or charging sound if you connect a charger
* The volume buttons do nothing outside of hardware tests and the mute switch also appears to do nothing 
* When flicking the mute switch you get no visual feedback, not in the Dynamic Island and not in a popover (think iOS 12 volume indicator)
* When pressing the volume buttons you also get no visual feedback
* When plugging in a charger, the haptic doesn’t play although other system haptics (like bringing up the accents on a keyboard key, or setting the mute switch to silent, or sliding your finger across options in a popup menu) do play
* This is another weird one, captive portal functionality is completely gone. Diagnostics mode will never show a captive portal login page, instead telling you that the Wi-Fi network can’t be used and that you should choose another network.
* Similar to this, the Wi-Fi settings are locked down. All you can do is connect to networks that are open, password protected or hidden, but the ‘i’ circle that shows IP address settings, DNS settings, proxy settings, etc is missing 
* Choosing to connect to a hidden network gets you an unrestricted keyboard where you can see that it has functioning autocorrect and emojis

All of these above observations are notably different compared to normal iOS, even compared to iOS in the Setup phase which makes you wonder just how much Apple removed from it compared to normal iOS.

I have yet to pick apart IPSWs, and I’m not even sure if the diagnostics mode is updated alongside the regular iOS install, but I’ll poke around in some IPSWs one of these days and make another blog post if I find anything interesting. Chances are that the diagnostics mode is just a fat ramdisk OS that iBoot boots into, which would explain all the weird changes and omissions.

I’d love to hear from others about this, so contact me at [thatstel.la](//thatstel.la) (hey maybe even join Fruitycord) if you want to chat!

Shairport Sync
=============
* Shairport Sync is an AirPlay audio player – it plays audio streamed from Apple devices and from AirPlay sources such [ForkedDaapd](http://ejurgensen.github.io/forked-daapd/).
* Shairport Sync can be built to support AirPlay 1 only or AirPlay 2. The AirPlay 2 build requires a good deal of extra library support and may not fit into smaller devices. AirPlay 2 also requires more CPU power and more RAM -- the minimum recommended device is a Raspberry Pi 3.
* **AirPlay 2 support is experimental and incomplete.** The focus of the development effort is on getting the best possible audio performance. Thus, many features that are outside that scope are missing or broken. So, for examples, integration with Apple's Home app is missing; remote control doesn't work.
* For AirPlay 2, Shairport Sync requires the services of another application called [NQPTP](https://github.com/mikebrady/nqptp) ("Not Quite PTP") for timing and synchronisation. NQPTP must run as `root` and must have exclusive access to ports `319` and `320`.
* When built for AirPlay 1, Shairport Sync runs on Linux, FreeBSD and OpenBSD.
* AirPlay 2 support is only available on recent Linux and FreeBSD builds. FreeBSD implementation has not been extensively tested.
* OpenBSD and Cygwin are not supported.
* AirPlay 2 support will definitely not work on Mac OS X. The reason is that Shairport Sync needs to use NQPTP, which uses ports `319` and `320`. These ports are  used by Mac OS X to support its implementation of AirPlay 2.

AirPlay 2 Issues
====
Did we mention AirPlay 2 support is experimental? You should also note that it is entirely possible that changes could be made that would stop Shairport Sync AirPlay 2 support from working. Let's hope that doesn't happen -- due to its limitations, there is little prospect of it having any kind of commercial significance.

What Works
---
* AirPlay 2 audio for players hosted on macOS and iOS.
* AirPlay 2 audio for System Sound Output from macOS.
* The `ALSA`, `stdout` and `pipe` backends definitely work, as does the `sndio` backend for FreeBSD.

What Does Not Work
---
* Shairport Sync AirPlay 2 can not be used from a PC or from an Apple TV.
* There is no integration with the Home app or HomeKit, so nothing to do with the Home app works.
* There is no integration with Siri.
* You can not run multiple instances of Shairport Sync on one device. This is because an instance of Shairport Sync requires exclusive access to NQPTP, and only one instance of that can run on a processor. (Docker may offer a workaround, but this has not been tested.)
* Remote Control from Shairport Sync back to the player doesn't work. The `D-Bus` interface is working, but anything requiring sending commands to the player doesn't work.
* Artwork is not downloaded.

More About What Works
---
* Two types of audio are received -- CD quality ALAC (like AirPlay 1) and AAC stereo at 44,100 frames per seconds. The selection of encoding is made by the player.
* Audio is synchronised with other AirPlay 2 devices, including AirPlay 2 devices that have their own master clocks. (Limitation: This has not been tested with multiple nearly-identical master clock devices such as with two HomePod minis -- Shairport Sync may get confused about which is the current master.)
* Shairport Sync continues to support AirPlay 1, and offers an AirPlay 1 compatibility mode for situations where iTunes or macOS Music plays to multiple speakers and one of more of them is compatible with AirPlay 1 only.

What You Need
---
* A Raspberry Pi 3 or better is needed. At present, Shairport Sync will not run on an original Pi or a Pi Zero.
* An extra program, NQPTP, is needed and must be run as `root`. It will use ports `319` and `320`, normally reserved for PTP clocks. If you are using PTP clock services for something else, you can't install NQPTP and so you can't use Shairport Sync.

Guides
---
* A brief guide to building Shairport Sync for AirPlay 1 is available at [BUILDFORAP1.md](https://github.com/aillwee/shairport-sync/blob/development/BUILDFORAP1.md).
* To build Shairport Sync for AirPlay 2 on Linux, please follow the guide at [BUILDFORAP2.md](https://github.com/aillwee/shairport-sync/blob/development/BUILDFORAP2.md).
* A guide for building on FreeBSD is forthcoming.

Note
---
Shairport Sync does not support AirPlay video or photo streaming.

More Information
---
For more information, and for a more complete account of how to build Shairport Sync for AirPlay 1, please visit [MOREINFO.md](https://github.com/aillwee/shairport-sync/blob/development/MOREINFO.md).

Acknowledgements
---
For the development of AirPlay 2 support, special thanks are due to:
* [JD Smith](https://github.com/jdtsmith) for really thorough testing, support and encouragement.
* [ejurgensen](https://github.com/ejurgensen) for advice and [code to deal with pairing and encryption](https://github.com/ejurgensen/pair_ap).
* [ckdo](https://github.com/ckdo) for pointing the way, particularly with pairing and encryption protocols, with a [functional Python implementation](https://github.com/ckdo/airplay2-receiver) of AirPlay 2.
* [invano](https://github.com/invano) for showing what might be possible and for initial Python development.
* [Charles Omer](https://github.com/charlesomer) for testing, encouragement and enthusiasm.

And of course, thanks to everyone who has supported and improved Shairport Sync over the years.

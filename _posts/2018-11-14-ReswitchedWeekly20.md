---
layout: post
title: Reswitched Weekly 20 
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

<!-- Something about radio silence here? -->

## What Happened: Some general tools

- @misson20000 released [Twili 1.0.0](https://github.com/misson20000/twili), which includes support for Firmware 5.0.0 and applet launching. It's also the first proper release.


## What Happened: Libtransistor Toolchain

- @misson20000 worked on improving libtransistor, including fixing a few annoying issues related to Firmware 5.0.0.

## What Happened: Libnx Toolchain

- @yellows8 added support for the video recording applet
- Actually, @yellows8, @fincs and many other contributors have worked hard on improving libnx. See the full commit log [here](https://github.com/switchbrew/libnx/commits/master).

## What Happened: Rust Toolchains

- @roblabla updated IPC definition and improved error handling in [MegatonHammer](http://github.com/megatonhammer/megaton-hammer).
- @ischeinkman created [libnx-rs](https://github.com/ischeinkman/libnx-rs), providing Bindings to libnx from rust, and also a full rust stdlib!


## What Happened: CTCAer's Hekate

- Hekate v4 was released! With it, support for chainloading was added, along with "Countless fixes and bugfixes" and other new features.
- Hekate v4.1 brough full 6.0.0 support, backlight brightness and backup cancellation.
- Hekate v4.2, the latest release supports wildcard kip loading, and cancellation of the backup verification process.

## What Happened: Atmosphère Custom Firmware

- @SciresM released Atmosphère! On October 17th, Atmosphère 0.7 was officially released, containing the fusée bootloader, the custom secmon exosphère and the widely used stratosphère sysmodules.
- Afterwards, Atmosphère versions 0.7.1 to 0.7.4 were released. They contained mainly bugfixes, but also performance improvements and the useful ability to see your Atmosphère version in the system settings.

## Call for participation

Reswitched is always looking for people to work on the various projects. If you
want to give a helping hand, hop on the [Discord] so we can coordinate the work!

If you want to work on Atmosphère, feel free to send a DM to @SciresM on
Discord. People can easily work on Fusée (getting the SDMMC driver to work, for
instance) by using Fusée-Gelée, or work on custom sysmodules, starting them with
nspwn or hekate's KIP injection.

In the libtransistor department, a lot of things could be implemented without
much requirements beyond "knowing C". Below are a list of issues, of varying
difficulty, that we feel the community could help on. If you're interested in
working on those, but need some help, feel free to reach out to @roblabla or
@misson20000 on Discord. We'll be glad to write some mentoring notes on what
needs to be done, and to guide you through the process.

- Documentation work!
  - Enhancing the libtransistor docs. You can take a look at
	[this issue](https://github.com/reswitched/libtransistor/issues/89).
  - SwIPC documentation. We need to make it *easy* for people to know what each
	function and service does.
- JIT API! We can call svcMapProcessCodeMemory, meaning we can
  JIT. See [here](https://github.com/reswitched/libtransistor/issues/119) if
  you'd like to pick this up.
- Thread Local Storage. Check [this issue](https://github.com/reswitched/libtransistor/issues/91).
- Implementing more services into libtransistor. We're lacking a bunch of things
  like NFC support and whatnot.
- Port apps and libraries. Make sure they work! We have graphics and audio, the
  sky is the limit!

## In two weeks...

If you're working on anything fun, please post on [next week's issue] on GitHub.
This way, I can include your stuff in here :D.

[next week's issue]: https://github.com/ReswitchedWeekly/ReswitchedWeekly.github.io/issues/42
[Discord]: https://discordapp.com/invite/DThbZ7z

---
layout: post
title: Reswitched Weekly 16
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

**TODO: Small blurb**

## What Happened: Some general tools

- Fusee Gelee got all kindsd of implementations. You can now hack your switch 
  [from Android](https://github.com/DavidBuchanan314/NXLoader),
  [from Windows](https://github.com/rajkosto/TegraRcmSmash),
  and even [from your web browser](https://github.com/atlas44/web-fusee-launcher).
  How scary is that?

- @rajtosko was on a roll: he relased [biskeydump](https://github.com/rajkosto/biskeydump) and [HacDiskMount](),
  allowing people to mount their NAND partitions from the comfort of their
  computers.

- @nwert released [Hekate-IPL](https://github.com/nwert/hekate), a bootloader
  that can load custom Kernels, trustzones, and inject KIP1s. You can imagine
  how useful that is ;).

## What Happened: The Libtransistor Toolchain

**TODO: Twili stuff I guess?**

## What Happened: Atmosphere Custom Firmware

- sdMMC support is going smoothly thanks to @ktemkin's perseverance. See
  [the alt_sdmmc branch](https://github.com/Atmosphere-NX/Atmosphere/tree/alt_sdmmc)
- Loader is fully re-implemented and works on hardware. [Check it out](https://github.com/Atmosphere-NX/Atmosphere/tree/master/stratosphere/loader)

## What Happened: Switch Linux
**TODO: Hopefully someone knows?**

## What Happened: RyujiNX Emulator
**TODO: Hopefully someone knows?**

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
working on those, but need some help, feel free to reach out to @roblabla on
Discord. I'll be glad to write some mentoring notes on what needs to be done,
and to guide you through the process.

- Documentation work!
  - Enhancing the libtransistor docs. You can take a look at
    [this issue](https://github.com/reswitched/libtransistor/issues/89).
  - SwIPC documentation. We need to make it *easy* for people to know what each
    function and service does.
- JIT API! We can call svcMapProcessCodeMemory, meaning we can
  JIT. We should make sure we have a proper API for this. Mimicking mprotect
  would probably be the best past, to be compatible with existing code.
- Joystick support in SDL2! If you want to pick this up, look at [this issue](https://github.com/reswitched/sdl-libtransistor/issues/1).
- Thread Local Storage. Check [this issue](https://github.com/reswitched/libtransistor/issues/91).
- Implementing more services into libtransistor. We're lacking a bunch of things
  like NFC support and whatnot.
- Port apps and libraries. Make sure they work! We have graphics and audio, the
  sky is the limit!

## In two weeks...

If you're working on anything fun, please post on [next week's issue] on GitHub.
This way, I can include your stuff in here :D.

[next week's issue]: TODO
[Discord]: https://discordapp.com/invite/DThbZ7z

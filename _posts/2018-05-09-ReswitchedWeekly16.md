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

- Fusée-Gelée got all kinds of implementations. You can now hack your switch 
  [from Android](https://github.com/DavidBuchanan314/NXLoader),
  [from Windows](https://github.com/rajkosto/TegraRcmSmash),
  and even [from your web browser](https://github.com/atlas44/web-fusee-launcher).
  How scary is that?

- @rajkosto was on a roll: he relased [biskeydump](https://github.com/rajkosto/biskeydump) and [HacDiskMount](),
  allowing people to mount their NAND partitions from the comfort of their Windows
  computers.

- @nwert released [Hekate-IPL](https://github.com/nwert/hekate), a bootloader
  that can load custom Kernels, trustzones, and inject KIP1s. You can imagine
  how useful that is ;).
  
- @SciresM added some new [Switch Tools](https://github.com/switchbrew/switch-tools)
  for converting ELF files to KIP1 as well as an [NPDM](http://switchbrew.org/index.php?title=NPDM)
  generator to build NPDM files from JSON.

  In the same vein, he also made hactool able to transform an NPDM into JSON.
  [Lookie here](https://github.com/SciresM/hactool/commit/fa2730ef598a2eb04ab7cbde6dcb957d0bcf1315).

## What Happened: The Libtransistor Toolchain

@misson20000 has been hard at work on Twili, a new, cleaner homebrew loader.
(Small interject: a homebrew loader and homebrew menu are totally different things).
It features:

- Loading NROs into clean-slate processes over USB
- Creating core dumps when they crash, which can be loaded into LLDB (requires a
  patch). GDB support is planned.
- Set custom resource limits on those processes (default memory limit is ~6MiB
  heap)
- Homebrew ABI shim that also gets loaded into the process. The HBABI shim gets
  loader config from Twili over IPC, ensuring HBABI compatibility.

This brought some libtransistor changes along to make sure everything worked:

- Removed `ace_loader`, as it is now obsolete
- Added waiters, for event-handling loops, with planned support for "signals"
  that don't depend on kernel event handles but can be signaled from other threads.
  It features a really cool C++ api to which you can pass lambda functions and
  the call to register an event returns a "WaitHandle" that will unregister when
  it gets destructed.
- Changed ipc server to use these waiters
- added template libraries for ipc client/server. See twili/IHBABIShim.cpp and
  twili/hbabi_shim.cpp for usage examples
- Removed `alloc_pages` since it's also obsolete
- added `runtime_config`, which are some weak symbols an application can use to
  override stdout/heap
- lots more C++ bindings
- changed C++ namespaces to be all lowercase and start with "trn" instead of
  "Transistor".

## What Happened: Atmosphère Custom Firmware

- sdMMC support is going smoothly thanks to @ktemkin's perseverance and it has now 
  made its way in to the main branch of [Atmosphère](https://github.com/Atmosphere-NX/Atmosphere/)
- @SciresM has finished fully reimplementing Loader. It requires more work to make it compatible with 2.x+ firmwares. [Check it out](https://github.com/Atmosphere-NX/Atmosphere/tree/master/stratosphere/loader)
- @SciresM is progressing on the PM reimplementation. [Check it out](https://github.com/Atmosphere-NX/Atmosphere/master/stratosphere/pm)

## What Happened: Switch Linux

Few things happened on the Switch Linux side. We're going to stay fairly
high-level: here's a taste of what's working, and what needs more work
(contributors welcome!):

- Display works correctly (some rootfs's need to manually rotate it)
  - Gnome has brightness support
- eMMC is accessible and can be dumped through dd or things like @daanhenke's [httpnand](https://github.com/daanhenke/httpnand)
- Bluetooth works (although it can be unstable)
- A linux joycon driver can be used to use bluetooth joycons as an input device
  - They do not work connected to console physically though. Contributors, take arm!
- Audio does not work
- USB does not work at all and charging is questionable (voltages may be wrong)
- Battery calibration is buggy for a lot of people.

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
working on those, but need some help, feel free to reach out to @roblabla or
@misson20000 on Discord. We'll be glad to write some mentoring notes on what
needs to be done, and to guide you through the process.

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

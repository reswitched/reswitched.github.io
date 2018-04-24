---
layout: post
title: Reswitched Weekly 15
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Almost two months happened, and boy was it a ride! Keys were leaked, bugs were
revealed, improvements were made.

## What happened: The Exploits

A number of exploits have been revealed in the past couple of weeks. We'll go
over them, what they allow and why they're important:

- expLDR allows crashing some sysmodules. When coupled with sm:h, this can be
  used to gain access to services that are limited to one connection, such as
  fsp-ldr.

  `fsp-ldr` is a particularly interesting target, because it allows us to gain
  full FileSystem permission, allowing to read and write anywhere we want. This
  can be leveraged to dump all the system modules, make a NAND backup, or write
  to various places (though that's a pretty fast road to the brick).

- nspwn is the exploit behind the homebrew launcher. fsp-ldr's `MountCode`
  function (which is used by the `Loader` when creating a process)
  supports more format than just NCA, and among them, it supports the NSP
  format, which doesn't have any signature. As a result, if we could get fsp-ldr
  to mount an NSP instead of the proper NCA, we could then make it load whatever
  code (with whatever permission) we desire.

  To get MountCode to load an NSP instead of the NCA, we need to change the NCA
  path. This is done with `lr`, the "Location Resolver". Thanks to the `sm:h`
  vulnerability, we can simply call `SetProgramNcaPath` to set the title's
  executable to our malicious NSP file.

- Fusee-Gelee, AKA shofel2, AKA Fuzzy Jellies, AKA Fussy Julie, AKA memecpy,
  AKA Recovery A La Mode, is a coldboot bootROM exploit. The short version of
  this exploit is that the USB parser feeds a user-controlled length to a
  memcpy. By making that length very big, we can override the application stack.
  Read [the whitepaper](https://github.com/reswitched/fusee-launcher/blob/master/report/fusee_gelee.md)
  to get all the details.

  This exploit is *big*, as it is basically a complete compromise of the Switch's
  security model. With it, we can dump the SBK, TSEC keys, and all kind of other
  private data. We can also use it to load an unsigend payload, paving the way
  for CFW.

## What happened: The libt toolchain

Libtransistor saw a number of improvement thanks to the epic work of @misson20000:

- @misson20000 added USB (Device Side) support, allowing the switch to
  communicate with a Host (like a PC). [See commit](https://github.com/reswitched/libtransistor/commit/1da51fe55c5c5f65d3435b35cb4be5c19490008b)

- Building on this, a usb-serial module was also added. It is possible to get an
  fd to it, allowing to redirect printf calls for easier debugging. [See commit](https://github.com/reswitched/libtransistor/commit/5402efbfac3299b52e3e84ae72d5fa6c9ba00ffb)

- Thread and mutex primitives were added.
  - Thread primitives can be found here: [See commit](https://github.com/reswitched/libtransistor/commit/7f7ac8586b30d77c3f6ec62318614427e2ba3bc2)
  - Mutexes: [See commit](https://github.com/reswitched/libtransistor/commit/5ee8dcc540beb87dd887eaf5af188202c99b509a)
  - And some work was done to ensure the thread safety of the existing components.

## What happened: Atmosphere Custom Firmware

Custom firmware is advancing at sonic speed. Let's go over what is planned:

- Fusee as a bootloader, with emunand creation menu
- Exosphere as TrustZone reimplementation, with CFW SMC GetInfo extensions.
- Thermosphere providing emunand via EL2
- Re-implementations and extensions of the Loader, sm, and boot system modules.
  - Loader: Extend to prefer "sdmc:/\<atmosphere dir\>/titles/title\_id/..."
    over "code:/..." when reading ExeFS, providing easy modification of any
    title's code.
  - SM: Extend with both an arbitrary service getter backdoor, and a "mitm"
    command that allows you to easily register yourself as a mitm for any given
    service.
  - boot: Provides an ideal place to initialize anything else in the system that
    we want to customize, and launch other custom sysmodules.

Current focus seems to have been on Loader - with SM and `exosphere` already
being fully functional replacements of their stock counterparts.

## What people are working on

- @roblabla is working on a standalone toolchain in rust, [Megaton Hammer](https://github.com/roblabla/megaton-hammer). Currently working on fixing the allocator.
- @misson20000 is working on Twili, a sysmodule launcher that will provide
  stdio and crash reporting.
- @misson20000 also got a toy dynamic loader into libtransistor, paving the way
  for dynamic cores in RetroArch and traNVparency improvements. [See PR](https://github.com/reswitched/libtransistor/pull/143)
- @ktemkin is working on the SDMMC driver for Atmosphere's Fusee. [See here](https://github.com/Atmosphere-NX/Atmosphere/blob/alt_sdmmc/fusee/fusee-primary/src/sdmmc.c)
- @SciresM is working on the custom Loader implementation.

## Call for participation

Reswitched is always looking for people to work on the various projects. If you
want to give a helping hand, hop on the [Discord] so we can coordinate the work!

If you want to work on Atmosphère, feel free to send a DM to @SciresM on
Discord. People can easily work on Fusee (getting the SDMMC driver to work, for
instance) by using Fusee-Gelee, or work on custom sysmodules, starting them with
nspwn.

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

## Next week...

If you're working on anything fun, please post on [next week's issue] on GitHub.
This way, I can include your stuff in here :D.

[next week's issue]: https://github.com/ReswitchedWeekly/ReswitchedWeekly.github.io/issues/35
[Discord]: https://discordapp.com/invite/DThbZ7z

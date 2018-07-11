---
layout: post
title: Reswitched Weekly 18
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Due to my excessive procrastination, this update is brought to you by @Gerd2002.
Maybe I should rename this blog to Reswitched Whenever. Or Reswitched
Spontaneously.

Anyways, during that month, the community made a huuuge progress on many fields.
We'll probably be missing things here, so we'll try to keep it to the major
events.

## What Happened: Some general tools

- @desowin did some work on SDMMC drivers
- @StevenMattera added touch input support to Homebrew Menu
- @Adubbz made [Gag Order](https://github.com/Adubbz/Gag-Order), an easy way to remove supernag
- [@perillamint](https://gitlab.com/perillamint) created [nx-fwextract](https://gitlab.com/perillamint/nx-fwextract)
  to use original firmware for bluetooth and wifi under linux
- A new hardmod has appeared! It's apparently possible to fit an Adafruit Trinket M0 inside of the switch.

## What Happened: Libtransistor Toolchain

- @misson20000 fixed tearing, implemented dynamic linking and USB, Serial and Stdio overrides
- @kbhomes implemented support for the NRO ASET header
- @roblabla fixed BSS cleaning

## What Happened: MegatonHammer Toolchain

- @roblabla resumed work, after a short break. (Some people say it was a revival)
- megaton-ipc has been merged into the megaton-hammer crate, in the ipcdefs module.
- Low-level IPC handling got a few bugfixes.
- Twili support has been added, giving us the possibility to redirect stdout to
  USB.

## What Happened: Hekate Bootloader

- @CTCaer is now maintaining Hekate. All the following updates were implemented by him
- Backup/Restore NAND
- Autoboot
- Fixed Sleep mode on 3.x series firmware.

## What Happened: Atmosphère Custom Firmware

- @neobrain cleaned up the code a little and modernized C++ usage
- @SciresM added LayeredFS support to Atmospère, allowing to override game files from SD card.
  It's not ready for general use yet, and there is a high danger of getting your console banned
  from online functionality if you do use it.
- In order to support the above feature, Fusee grew support for Kernel Patches.
- @SciresM added a creport reimplementation, which writes crash reports to the
  SDCard instead of sending them to Nintendo.

## What Happened: Switch Linux

- Fixes for the battery desync issues have been commited to most maintained switch linux distros
- Lakka now runs on the Switch, thanks to the @lakka-switch project

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

[next week's issue]: https://github.com/ReswitchedWeekly/ReswitchedWeekly.github.io/issues/39
[Discord]: https://discordapp.com/invite/DThbZ7z

---
layout: post
title: Reswitched Weekly 17
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

## What Happened: Some general tools

- @roblabla made some kernel patches, allowing the use of various debug
  syscalls. See [the gist](https://gist.github.com/roblabla/440f3ceaa0b2d3ca530c2a43fe258420).
- @fincs fixed nx-hbloader so that it can now be used alongside games. Note that
  this change limits the size of the heap to 500MB.
  [Relevant commit](https://github.com/switchbrew/nx-hbloader/commit/d6e56d487f4624237407c395b93d53bfa6e44cf6)
- @roblabla is working on GDB integration in twili. **TODO: PR here**

## What Happened: Libtransistor Toolchain

**TODO: Anything?**

## What Happened: MegatonHammer Toolchain

- @Thog made a pure rust reimplementation of elf2nxo that's a lot more robust.
  [Check it out](https://github.com/MegatonHammer/elf2nxo).
- @Kitlith made the Megaton-Hammer IPC heapless, making its performance more
  predictable. See [the PR](https://github.com/MegatonHammer/megaton-hammer/pull/27).
- @roblabla updated Megaton-Hammer to Rust 1.26.

## What Happened: Atmosphère Custom Firmware

**TODO: Anything?**

## What Happened: Switch Linux

- Audio drivers were added! [See this commit](https://github.com/tardyp/switch-linux/commit/9ab9a019fdf1275f1dd6b911bd7f37cb49738cbe)
- @shinyquagsire23 got joycons to work (docked) in switch linux. The patches can
  be found [here](https://github.com/shinyquagsire23/Switch-Linux/commit/1580857997fb6d77f2f9b63f23d95ad68f420210).


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


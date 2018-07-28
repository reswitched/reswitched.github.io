---
layout: post
title: Reswitched Weekly 19
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a bi-weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

## What Happened: Some general tools

- @misson20000 released [Ilia](https://github.com/misson20000/ilia), a tool to
  MITM and log all IPC activity on your Switch.
- @Adubbz released [tinfoil](https://github.com/Adubbz/Tinfoil), a tool that
  should eventually allow the installation of Homebrew on the Home Menu.

## What Happened: Libtransistor Toolchain

- Libtransistor 2.0.0 is officially out.
- @misson20000 fixed 1.0.0 usb bindings.

## What Happened: MegatonHammer Toolchain

- [MegatonHammer](http://github.com/megatonhammer/megaton-hammer) now uses proper
  kernel mutexes for its internal synchronization instead of spinlocks. The commit [here](https://github.com/MegatonHammer/megaton-hammer/commit/1d3d27fb5553965456671e4ff9ecb827071e5735)
- @roblabla is working on a pure-rust unwinder so that we may unwind the stack. [Check it out](https://github.com/roblabla/unwind-rs).
  in homebrew.
- @Thog added buildid support in Linkle (our pure-rust elf2nxo). The commit [here](https://github.com/MegatonHammer/linkle/commit/13c25eae62cc960ed124475221c7971f4353d20a)

## What Happened: CTCAer's Hekate

- @rajkosto added a kip patching mechanism. See [here](https://github.com/CTCaer/hekate/pull/51).

## What Happened: Atmosphère Custom Firmware

- @SciresM embedded boot2 logic into PM.
- @SciresM added the ability to specify custom boot2 launch titles.
- @SciresM added the ability to MITM (some) system titles.
- @hexkyz deployed a new SDMMC driver in fusee-secondary, allowing it to boot
  properly.

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

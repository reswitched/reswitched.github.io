---
layout: post
title: Reswitched Weekly 2
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, some attention was given to Mephisto, pthread and C++ support.

## What was done

Not much was actually finished this week. But a lot of stuff was worked on.

## What people are working on

- [roblabla](https://github.com/roblabla) enhanced File Descriptor table to
  be atomic and thread-safe [newlib#2](https://github.com/reswitched/newlib/pull/2).
- [roblabla](https://github.com/roblabla) is porting OpenBSD's `pthread` library
  for the switch. This will give a common, standard API for creating threads,
  mutexes, semaphores, and spinlocks. Lots of wizardry abound.
  [libtransistor#48](https://github.com/reswitched/libtransistor/pull/48)
- [dvdfreitag](https://github.com/dvdfreitag) is working on building LLVM's libc++
  for C++ support in libtransistor.
- [roblabla](https://github.com/roblabla) added multithreading support to
  Mephisto, and fixed a couple papercuts.
  [mephisto#15](https://github.com/reswitched/Mephisto/pull/15)
- [kgsws](https://github.com/kgsws) is working on Switch Doom, implementing
  client-server multiplayer.
- Work is still ongoing for GPU/Audio support.

## What happened outside Reswitched

Two important releases were done by Yellows8 and plutoo:

- [`nxdbg`](https://github.com/switchbrew/nxdbg), a debugger for the Nintendo
  Switch. It requires a private kernelhax to be used.
- A way to get webkit access with the Switch firmware 1.0.0, through the JPN
  version of Puyo Puyo Tetris. [See here](http://switchbrew.org/index.php?title=Internet_Browser#WebApplet_launch_with_Tetris).

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Thread Local Storage, by implementing emutls.
- Implementing more services into libtransistor.
- Port some apps, like micropython, and make sure they work !

---
layout: post
title: Reswitched Weekly 2
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, some attention was given to Mephisto, pthread and C++ support.

## What was done

Not much was actually finished this week. But a lot of stuff was worked on.

## What people are working on

- roblabla enhanced his File Descriptor table to be atomic and thread-safe
  [newlib#2](https://github.com/reswitched/newlib/pull/2).
- roblabla is working on porting OpenBSD's `pthread` library for the switch.
  This will give a common, standard API for creating threads, mutexes,
  semaphores, and spinlocks. Lots of wizardry abound.
- dvdfreitag is working on building libstdcxx, for C++ support in libtransistor.
- roblabla added multithreading support to Mephisto, and fixed a couple
  papercuts.

## Wider community

Yellows8 and plutoo released two things:

- `nxdbg`, a debugger for the Nintendo Switch kernel. It requires a privat
  kernelhax, but still cool !
- A way to get webkit access with the Switch firmware 1.0.0, through the JPN
  version of Puyo Puyo Tetris.

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Thread Local Storage, by implementing emutls.
- Implementing more services into libtransistor.
- Port some apps, like micropython, and make sure they work !

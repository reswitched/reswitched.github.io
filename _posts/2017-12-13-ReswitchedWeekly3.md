---
layout: post
title: Reswitched Weekly 3
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, some more attention was given to C++ support and pthread.

## What people are working on

- @dvdfreitag managed to compile libcxx, libcxxabi and libunwind for the
  Nintendo Switch. C++ support is almost palpable.
- @TurtleP started porting [LovePotion](https://github.com/TurtleP/LovePotion/tree/switch)
  to the Nintendo Switch. LovePotion allows writing games using a simple lua
  API.
- @roblabla spent his week fighting bugs in his pthread port.
- @misson20000 is still working on getting framebuffer support into
  libtransistor.
- @Pokemod97 is  writing a tutorial on setting up a proper development
  environment for libtransistor. Stay tuned !

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Thread Local Storage, by implementing emutls.
- Implementing more services into libtransistor.
- Port some apps, like micropython, and make sure they work !
- Documentation ! We have lots of moving parts that aren't properly documented.
  Setting up doxygen for `libtransistor` would be a huge first step towards
  fixing this. Writing some documentation for toolchain setup and `ace_loader`
  usage would be awesome too.

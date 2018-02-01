---
layout: post
title: Reswitched Weekly 10
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

After the fairly eventful week we had, things are settling down again. C++
support is finally in a working state, and libtransistor got some
S T A B I L I T Y.

## What happened

- @dvdfreitag's CPP port is now working! Well, almost. Exception-handling is
  broken.
- @misson20000 got filesystem merged into master ! This involved changing the
  squashfs compression method, which should now be easy to use.
- Speaking of master, *it disappeared*! We now have a stable branch that should
  only contain thoroughly tested code, and a development branch with the latest,
  potentially less well-tested goodies.

## What people are working on

- @Daeken is working on 3D graphics. He got an ELF loader to work on the switch,
  loading the nvidia tegra libraries. It now needs wrappers to be made. See [the
  code](https://github.com/daeken/traNVparency) and a
  [todo](https://checkvist.com/checklists/658460-tranvparency?widget=true).
- @roblabla is beating [libtransistor-rs](https://github.com/roblabla/libtransistor-rs)
  back into shape.
- Stary is porting Bochs (an x86 emulator) on the Nintendo Switch.

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work. Also, if you feel like you need mentoring notes on some of
those tasks, feel free to ping @roblabla on discord, I can write up what
needs to be done, and guide you through the process:

- Documentation work!
  - Enhancing the libtransistor docs. You can take a look at
    [this issue](https://github.com/reswitched/libtransistor/issues/89).
  - SwIPC documentation. We need to make it *easy* for people to know what each
    function and service does.
- Joystick support in SDL2! If you want to pick this up, look at [this issue](https://github.com/reswitched/sdl-libtransistor/issues/1).
- Thread Local Storage. Check [this issue](https://github.com/reswitched/libtransistor/issues/91).
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Port apps and libraries. Make sure they work! We have graphics and audio, the
  sky is the limit!

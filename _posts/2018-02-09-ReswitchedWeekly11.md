---
layout: post
title: Reswitched Weekly 11
1ategory: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, @SciresM released some new tools. New, shiny tools.

## What happened

- @SciresM released [hactool](https://github.com/sciresm/hactool), allowing to
  view information about, decrypt, and extract common file formats for the
  Switch. You need to Bring your own Keys!
- @SciresM also released a [KIP1 loader](https://github.com/reswitched/loaders),
  allowing easy reverse engineering of builtins.
- @DavidBuchanan314 added touchscreen support to libtransistor!
  [See the PR](https://github.com/reswitched/libtransistor/pull/94).

## What people are working on

- @Daeken is working on 3D graphics, see [traNVparency](https://github.com/daeken/traNVparency).
  To make his work easier, he patched nxdbg to include a CLI UI and a network
  interface. See [here](https://github.com/daeken/nxdbg).

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

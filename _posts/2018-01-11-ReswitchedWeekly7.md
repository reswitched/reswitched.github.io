---
layout: post
title: Reswitched Weekly 7
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, not a whole lot has happened. Lots of work going on behind the
scenes, while everyone is waiting for nvace.

## What people are working on

- @vgmoose finished his Space Game port for the switch.
  [Check it out](https://github.com/vgmoose/spacenx).
- Lots of people are hard at work trying to make various RetroArch emulator
  cores work with libtransistor.
- @3Daniel is working on setting up Doxygen documentation.
- @kgsws is working on his multiplayer doom port.
- @roblabla is busy trying to find a way to get backtraces to debug his numerous
  crashes.

## What happened in the broader community

- @GovanifY implemented the ldr:ro crash (first revealed in 34C3) in pegaswitch.
  It allowing dumping the sysmodules' code ! He wrote an easy-to-read writeup of
  the vulnerability, [check it out](https://govanify.com/post/switch-interlude/) !
  And here's the associated [Pull Request](https://github.com/reswitched/pegaswitch/pull/81)
  for pegaswitch. (Note that it's for 2.0.0-consoles only right now, but it
  could be extended to any version < 3.0.0).

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work. Also, if you feel like you need mentoring notes on some of
those tasks, feel free to ping @roblabla on discord, I can write up what
needs to be done, and guide you through the process :

- Joystick support in SDL2 !
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Thread Local Storage, by implementing emutls.
- Port apps and libraries. Make sure they work ! We have graphics and audio, the
  sky is the limit !

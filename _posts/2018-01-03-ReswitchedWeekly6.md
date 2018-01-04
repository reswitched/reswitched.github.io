---
layout: post
title: Reswitched Weekly 6
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Happy new years everybody ! Now that we've got graphics and audio support up and
running, the community started to go at full speed, porting games, libraries and
emulators at an increasingly fast pace. Here are some highlights of what's going
on !

## What people are working on

- @Thog is working on a port of the atari800 emulator for the switch !
[Check it out !](https://github.com/Thog/atari800-switch)
- @Maschell created a "Push the button" game, a nice and simple example of how
  to use the SDL library to draw on the screen, and how to use the HID library.
  [Take a look](https://github.com/Maschell/PushA_NX).
- @vgmoose is porting a WiiU homebrew to the Switch ! It's a space game ! It's
  [on github](https://github.com/vgmoose/spacenx).
- @kgsws is working on a homebrew launcher, using HTTP to download NROs from
  pegaswitch.
- @misson20000 is working on the networked FS and general FS structure as well.
- @roblabla is still hard at work on SaveFS.

## What happened in the broader community

- @hedgeberg did a Q/A about Glitching the switch, and what it entails. You can
  get the audio [there](https://mirror.ktemkin.com/binsmash/fault_injection_qa_1_1_18.mp3)
  (it starts after 15 seconds). This should answer all your questions about what
  glitching does.
- For the record, the 34C3 video was reuploaded after it was taken down. You can
  find it [here](https://www.youtube.com/watch?v=Ec4NgWRE8ik). This is a
  must-watch for everybody !

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work. Also, if you feel like you need mentoring notes on some of
those tasks, feel free to ping @roblabla on discord, I can write up what
needs to be done, and guide you through the process :

- Documentation ! We have lots of moving parts that aren't properly documented.
  Setting up doxygen for `libtransistor` would be a huge first step towards
  fixing this. We also need help writing tutorials for Mephisto and other tools.
- Joystick support in SDL2 !
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Thread Local Storage, by implementing emutls.
- Port apps and libraries. Make sure they work ! We now have graphics and audio,
  the sky is the limit !

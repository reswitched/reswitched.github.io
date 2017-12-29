---
layout: post
title: Reswitched Weekly 5
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week started rather slow, with not much happening due to the holiday
season. But on the 28th, the 34C3 happened, and we got **lots of good stuff**

## What was merged

- @misson20000 pushed framebuffer and audio support ! We can now display stuff,
  and play sounds ! Games are finally happening !
- @misson20000 also released a SNES emulator, based on
  [RetroArch](https://github.com/reswitched/RetroArch)
  and [snes9x2010](https://github.com/reswitched/libtransistor-snes9x2010).
- @Pokemod and @roblabla wrote a tutorial to setup a working Switch Homebrew
  development environment,
  [check it out](https://reswitchedweekly.github.io/Development-Setup/).

## What people are working on

- @misson20000 will be working on the FS abstraction layer, implementing FS
  mounts, writing an SMB client, and sharing FS mounts between apps.
- @kgsws added framebuffer support in his Doom port. He's working on getting
  analog controls, and fixing the occasional crashes.
- @roblabla is going to be busy working on the FS abstraction layer,
  implementing "save FS" mounts.

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Documentation ! We have lots of moving parts that aren't properly documented.
  Setting up doxygen for `libtransistor` would be a huge first step towards
  fixing this. We also need help writing tutorials for Mephisto and whatnot.
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Thread Local Storage, by implementing emutls.
- Port apps and libraries. Make sure they work ! We now have graphics and audio,
  the sky is the limit !

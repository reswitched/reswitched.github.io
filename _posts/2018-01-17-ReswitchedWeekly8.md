---
layout: post
title: Reswitched Weekly 8
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Too much happened this week. Lots of releases.

## What happened

- @SciresM confirmed TZhax working on 1.0.0-3.x. This means complete system
  access on those firmwares. (Do not use that excuse to upgrade your switch.
  Lower versions will get stuff faster, and lower is still better. Each time a
  Switch gets updated, a puppy dies).
- A new Nintendo Switch emulator, [yuzu](https://yuzu-emu.org/), made its
  appearance. It is open source, made by the same team as citra, is able to
  run homebrew (though not at playable speed), and has a neat GDB stub debugger!
  Should make for a nice Mephisto replacement.
- @3Daniel's documentation work got merged. The libtransistor documentation is
  now [live](https://reswitched.github.io/libtransistor/).
- @roblabla's first batch of SwIPC documentation work got merged.
  [PR](https://github.com/reswitched/SwIPC/pull/13)
- @corenting fixed various python script in libtransistor to work with both Py2
  and Py3. [PR](https://github.com/reswitched/libtransistor/pull/83)

## What people are working on

- @Daeken started porting the Linux4Tegra GPU driver.
- @dvdfreitag is finishing up his C++ work
- @misson20000 is working on implementing hb-abi, which will allow libnx and
  libtransistor to stay compatible.
  [PR](https://github.com/reswitched/libtransistor/pull/84)
- @roblabla is working on further SwIPC improvements in regards to docs.
  [PR](https://github.com/reswitched/SwIPC/pull/14)

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work. Also, if you feel like you need mentoring notes on some of
those tasks, feel free to ping @roblabla on discord, I can write up what
needs to be done, and guide you through the process:

- Documentation! Enhancing the libtransistor docs, and documenting all the
  SwIPC methods! We need to make it *easy* for people to know what each
  function does.
- Joystick support in SDL2!
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Thread Local Storage, by implementing emutls.
- Port apps and libraries. Make sure they work! We have graphics and audio, the
  sky is the limit!

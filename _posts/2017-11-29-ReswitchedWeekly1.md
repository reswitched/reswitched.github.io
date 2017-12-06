---
layout: post
title: Reswitched Weekly 1
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Most of the work done this week involved kgsws's `ace_loader`. This software
is tasked with multiple jobs : it has to clean up the browser environment, and
allow loading more NROs through a TCP server. It will also set up stdio to
route to a telnet server. The long term goal is to have graphic homebrew
launchers use aceloader as the service to start apps.

## What was done

- [kgsws](https://github.com/kgsws) and [misson20000](https://github.com/misson20000)
  got stdio support into `libtransistor`, routing through a TCP stream.
- It is now possible to pass arguments when loading NROs.
- [dvdfreitag](https://github.com/dvdfreitag) has integrated `libssp` into
  `libtransistor`, giving us working stack guards. Our programs are safe from
  stack smashing now !
- [misson20000](https://github.com/misson20000) has integrated `compiler-rt`
  into `libtransistor`, fixing various hurdles related to missing symbols.
- A rather big cleanup of the Makefiles were done.

## What people are working on

- [kgsws](https://github.com/kgsws) is working on getting Doom running. He got
  it to run, sending rendered GPU frames to a PC ! He got input working too,
  through libtransistor's HID support !
- Graphics and audio support are being worked on by various members of the
  community, including [misson20000](https://github.com/misson20000). According
  to last update, "`am` (Applet Manager), responsible for taking a framebuffer
  and drawing global widgets to it, uses `pdm:ntfy`, which is part of `sdb`,
  which our ACE kills."
- [roblabla](https://github.com/roblabla) is working on getting a File Descriptor
  table into `newlib`, to properly implement FD-related syscalls (such as `read`
  and `write`).

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Pthread emulation layer
- Thread Local Storage, by implementing emutls
- Implementing more services into libtransistor

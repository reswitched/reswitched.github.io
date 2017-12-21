---
layout: post
title: Reswitched Weekly 4
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

This week, we started working on File System support, and various libs were
ported.

## What was merged

- @roblabla's File Descriptor support is now merged. We can now create bsd
  sockets through the normal libc function, and do a couple of "standard"
  file-descriptor operations on them (`dup2`, `close`, etc...)

## What people are working on

- @misson20000 is working on Virtual FileSystem support, one small step at a
  time. A prototype lives in
  [#61](https://github.com/reswitched/libtransistor/pull/61).
- @maci0 created a docker image for pegaswitch and mephisto, you can get it
  [there](https://hub.docker.com/r/reswitched/).
- @kgsws managed to get liblua up and running on the switch, it didn't require
  any modifications ! He's also busy adding features to his Doom port.
- @maci0 got zlib to compile as well. You can grab the recipe
  [here](https://github.com/maci0/switchports).
- @roblabla is still busy with 
  [pthread](https://github.com/reswitched/libtransistor/pull/48).

## Call for participation

Lots of things could be implemented properly into libtransistor/newlib without
much more reverse-engineering. If you're a developer and want to give a hand,
make sure to hop on [Discord](https://discordapp.com/invite/DThbZ7z) so we can
coordinate work.

Things that need work on :

- Thread Local Storage, by implementing emutls.
- Implementing more services into libtransistor.
- Port apps and libraries, like micropython, and make sure they work !
- Documentation ! We have lots of moving parts that aren't properly documented.
  Setting up doxygen for `libtransistor` would be a huge first step towards
  fixing this. Writing some documentation for toolchain setup and `ace_loader`
  usage would be awesome too.


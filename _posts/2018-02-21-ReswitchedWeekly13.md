---
layout: post
title: Reswitched Weekly 13
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

We're doing two weeks for the price of one this time. SciresM started working on
his CFW, Atmosphère. The Switchbrew team released HBL. Lots of interesting
developments.

## What happened

- Switchbrew team released [nx-hbexploit300], a 3.0.0 loader that works *much*
  better than ROhan! Among other things, it allows us to access the SD card, and
  a bunch of new syscalls, such as `svcMapProcessCodeMemory` (useful for JIT) or
  `svcReplyReceive` (useful to create custom services). To complement this, they
  also released [nx-hbmenu], the "official" Homebrew Menu.

- In light of this, @misson20000 fixed a couple bugs in libtransistor to make it
  compatible with the new hbl.

- @SciresM started working on [Atmosphère-NX] - specifically Exosphère, the
  TrustZone reimplementation. You can see his roadmap in the [Github Project]

## What people are working on

- @roblabla is working on bringing SD Card support to libtransistor. [PR 109]
- @roblabla also did a bunch of fixes to his SwIPC code generator. [PR 9]
- @misson20000 is splitting up the `ace_loader` into multiple modules. [PR 103]
- @TuxSH is working on porting FTPd to the switch. This is very useful for
  developers who want to reduce their edit-build-test cycle. Look at the
  [switch_pr] branch.
- @TurtleP is working on LovePotion. Work is ongoing in the input handling
  department. Look at LovePotion's [switch branch]

## Call for participation

Reswitched is always looking for people to work on the various projects. If you
want to give a helping hand, hop on the [Discord] so we can coordinate the work!

More specifically, if you're interested in working on Atmosphère and have the
relevant experience, send a DM to @SciresM on Discord.

In the libtransistor department, a lot of things could be implemented without
much requirements beyond "knowing C". Below are a list of issues, of varying
difficulty, that we feel the community could help on. If you're interested in
working on those, but need some help, feel free to reach out to @roblabla on
Discord. I'll be glad to write some mentoring notes on what needs to be done,
and to guide you through the process.

- Documentation work!
  - Enhancing the libtransistor docs. You can take a look at
    [this issue](https://github.com/reswitched/libtransistor/issues/89).
  - SwIPC documentation. We need to make it *easy* for people to know what each
    function and service does.
- JIT API! The new hbl allows us to call svcMapProcessCodeMemory, meaning we can
  now JIT. We should make sure we have a proper API for this. Mimicking mprotect
  would probably be the best past, to be compatible with existing code.
- Joystick support in SDL2! If you want to pick this up, look at [this issue](https://github.com/reswitched/sdl-libtransistor/issues/1).
- Thread Local Storage. Check [this issue](https://github.com/reswitched/libtransistor/issues/91).
- Implementing more services into libtransistor. We're lacking a bunch of things
  like USB support and whatnot.
- Port apps and libraries. Make sure they work! We have graphics and audio, the
  sky is the limit!

## Next week...

If you're working on anything fun, please post on [next week's issue] on GitHub.
This way, I can include your stuff in here :D.

[nx-hbexploit300]: https://github.com/switchbrew/nx-hbexploit300
[nx-hbmenu]: https://github.com/switchbrew/nx-hbmenu
[Atmosphère-NX]: https://github.com/sciresm/Atmosphere-NX
[Github Project]: https://github.com/SciresM/Atmosphere-NX/projects
[PR 109]: https://github.com/reswitched/libtransistor/pull/109
[PR 103]: https://github.com/reswitched/libtransistor/pull/103
[switch_pr]: https://github.com/TuxSH/ftpd/tree/switch_pr
[switch branch]: https://github.com/TurtleP/LovePotion/tree/switch
[PR 9]: https://github.com/reswitched/SwIPC/pull/9
[next week's issue]: https://github.com/ReswitchedWeekly/ReswitchedWeekly.github.io/issues/27
[Discord]: https://discordapp.com/invite/DThbZ7z

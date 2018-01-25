---
layout: post
title: Reswitched Weekly 9
category: reswitchedweekly
---

Hello and welcome to Reswitched Weekly, a weekly summary of the progress
made by the reswitched team and wider community around homebrew development for
the Nintendo Switch.

Another eventful week ! Hacks were written up, emulators were ported, work was
done.

## What happened

- @SciresM published a writeup of his 1.0.0 tzhax, called "jamais vu". You
  really should go read it [here](https://www.reddit.com/r/SwitchHacks/comments/7rq0cu).
  And for those following us at home: You'll know if you got jamais vu working
  right if
  ```
  sha512(master_key for 1.0.0-2.3.0) == AD4E1C54708214F661D95AA97A47A71EDF63D3CE3B358282B5665DA67E2FE6616D263D17C9E750DE38845AB0F3F4DD5032E7E4030741B59A0A71B6B34AB9F331
  ```

- @SciresM also released `NCA tool`, a tool allowing manipulation and decryption
  of NCAs. You need to bring your own keys.
  [Check it out](https://github.com/SciresM/ncatool).

- @misson20000 implemented the hb-abi, which allows libnx and libtransistor to
  be compatible at the loader level!
  [PR](https://github.com/reswitched/libtransistor/pull/84).

  **NOTE**: You will need to update pegaswitch, libtransistor and ace_loader,
  and recompile all your NROs with this new change. It is a breaking,
  backward-incompatible change.

- A major bug uninitialized memory bug was fixed in RetroArch, making it a lot
  more stable. [Commit](bb1fdad0d983adc96de337a05546ed9eb99911ed)

- Thanks to the fix above and great work from @lubosz, Yabuse (a Sega Saturn
  retroarch core) is now in a working (albeit slow) state.

- @endrift fixed the MacOS builds! It is now possible to use libtransistor on
  MacOS. The guide was updated, it now has steps for MacOS users.
  [PR](https://github.com/reswitched/libtransistor/pull/85)

## What people are working on

- @Daeken started porting the Linux4Tegra GPU driver.
- @dvdfreitag is finishing up his C++ work. You can check it out
  [there](https://github.com/dvdfreitag/libtransistor), but keep in mind it
  doesn't quite work yet.
- @roblabla's SwIPC improvements moved along. 300 functions got named (only 1200
  functions left to name), and ~200 functions got some documentation ported over
  from switchbrew. [PR](https://github.com/reswitched/SwIPC/pull/14)

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

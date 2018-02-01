---
layout: post
category: tutorial
title: Building RetroArch
---

In this article, we'll go through the process of building RetroArch and the 
Snes9x-2010 core for the nintendo switch.

It is assumed that you have already completed all of the setup steps outlined
in the [Development Environment Setup Guide](https://reswitchedweekly.github.io/Development-Setup/).

Disclaimer: The instructions in this section relate to projects that are under
active development. These instructions will probably become out of date quickly.

Credit to Mission20000 for the original work on these ports.

## Limitations:

- The snes roms are currently compiled inside the nro file. Therefore you must compile 
a new copy of the emulator every time you want to add or remove roms.
- Input / controls are still under development. They may work well, or not at all. 
This is NOT a bug.
- Switch Joycons must be used in detached mode (NOT connected to the sides of the
Switch console otherwise the input / controls won't work.
- You will probably need to reboot the console to quit the game / emulator.
- You can attempt to build other cores for RetroArch than Snes9x, but many will fail due to 
requirements such as needing to use the file system, or needing specific graphics
systems. Some cores for newer systems such as N64, PSX etc are not able to run yet, even 
if you could build them.

## Snes9x-2010

Before being able to build RetroArch, we need to build the Snes9x-2010 core. But before
building the Snes9x-2010 core, we have to ensure that we are using the correct branch of
libtransistor. While graphics have now been merged into the main libtransistor, there are
still some file system related things that are still pending as of 2018/02/01.

In order to compile RetroArch, you will first need to get the 
[fs](https://github.com/reswitched/libtransistor/tree/fs) branch of libtransistor and 
compile it. If you already have libtransistor checked out, you can simply `git checkout 
origin/fs`. Or if you would rather checkout just the specific branch, you can use `git 
clone --recursive -b fs https://github.com/reswitched/libtransistor.git`. 
Once you have the branch checked out, you can run `make` on libtransistor.

Troubleshooting:
- I'm getting an error about `implicit declaration of function 'closedir'` or `<dirent.h> 
  not supported` or `unknown type name 'DIR'`?

  See the section below about updating submodules.

- I'm getting an error about `libtransistor/sdl2/configure: not found` or `libtransistor/build
/sdl2/Makefile' failed`?

  The SDL2 submodule hasn't been updated properly. See the section below about
  updating submodules.

### Updating Submodules

The fs branch of libtransistor uses a different revision of the newlib 
submodule, which includes a working dirent.h header. Run `git submodule update`. If that 
doesnt work, try `git submodule update --init --recursive`. If that still hasn't properly 
updated the submodules then you may need to try just checking out the specific branch into 
a new directory: `git clone --recursive -b fs 
https://github.com/reswitched/libtransistor.git`.

Once you have built the fs branch of libtransistor, you can now move 
on to Snes9x. Checkout [libtransistor-snes9x2010](https://github.com/reswitched/libtransistor-snes9x2010)
and make it as follows:

```
git clone https://github.com/reswitched/libtransistor-snes9x2010.git
cd libtransistor-snes9x2010
make platform=switch LIBTRANSISTOR_HOME=/path/to/libtransistor/fs/branch
```
Depending on whether you already set an environment variable for LIBTRANSISTOR_HOME, you 
may need to put the path in to the make command as well. Ensure that the path is to the 
fs branch that you have just built.

When it has successfully finished building, you will have a file called `snes9x2010_libretro_switch.a`
in your libtransistor-snes9x2010 folder.


## RetroArch

Next up is building [RetroArch](https://github.com/reswitched/RetroArch

```
git clone https://github.com/reswitched/RetroArch.git
cd RetroArch

# Create a new folder called fs
mkdir fs

# Move the snes9x2010_libretro_switch.a file we built before into the libtransistor-retroarch 
# folder and rename it to libretro_switch.a
mv /path/to/libtransistor-snes9x2010/snes9x2010_libretro_switch.a ./libretro_switch.a
```

You are just about ready to go, but first you need to find at least one snes rom file (no, we 
won't tell you where to get them, do not ask) and copy it into the fs folder that we just created.
Once the rom file is in the fs folder, rename the file so that the name does NOT contain any spaces.
If you want to include more than one rom file, just place them all into the fs folder before building.

Now you are ready to make it: `make -f Makefile.switch LIBTRANSISTOR_HOME=/path/to/libtransistor/fs/branch`

You can now take the resulting `retroarch_switch.nro` file and load it via PegaSwitch and ace_loader.
Then from the RetroArch menu screen, select `Load Content`, navigate to the `/` folder and select the rom
that you'd like to play.

If you decide you want to rebuild it to try different roms, be sure to delete both the `retroarch_switch.nro` 
file as well as the `fs.squashfs` files before rebuilding.

Troubleshooting:
- I'm getting an error `ld.lld-5.0: error: libretro_switch.a(libretro.o) is incompatible with version_git.o`

  This means that you probably didn't build `libtransistor-snes9x2010` properly. Go back and ensure you
  build it with the correct platform. Then re-copy the `libretro_switch.a` file into the `libtransistor-retroarch`
  folder.

- I'm getting an error `No rule to make target 'libretro_switch.a', needed by 'retroarch_switch.nro.so'.  Stop.`.

  This happens when you are missing the `libretro_switch.a` file from the `libtransistor-retroarch` folder.

- I'm getting an error `No rule to make target 'fs/', needed by 'fs.squashfs'. Stop.`.

  This happens because your `fs` folder is empty. You need to put at least one
  ROM in there for RetroArch to compile properly.


## Where to go from here:

You should now have a working Snex9x RetroArch which can run on your Switch!

If you are willing to give us a helping hand, don't hesitate to join our
[Discord](https://discordapp.com/invite/DThbZ7z). There is a lot of work left to
be done, lots of emulators need to be ported. It's time to Emulate All the
Things !

### Last Updated: 2018/01/06

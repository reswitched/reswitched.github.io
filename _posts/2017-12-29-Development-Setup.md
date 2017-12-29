---
layout: post
category: tutorial
title: Development Environment Setup
---

In this article, we'll look at what it takes to set up a development environment
for the nintendo switch. The steps here describe the (un)officially supported
way to build Homebrew.

You will need an ArchLinux, Debian or Ubuntu (other OSes coming soon), and a
Switch with the 3.0.0 firmware. You'll also need git.

## PegaSwitch

The first thing you'll need is the tools to exploit vulnerabilities on the
Switch. For this, we use PegaSwitch, an exploit framework. To install PegaSwitch,
you need a modern version of Node.JS. You can follow the tutorial on the
[Node.JS website](https://nodejs.org/en/download/package-manager/).

You then need to clone and install PegaSwitch.

```
git clone https://github.com/reswitched/pegaswitch
cd pegaswitch
# Install the pegaswitch dependencies
npm i
# Start pegaswitch
sudo node start.js 
```

This will create a DNS and HTTP server on your computer, that your switch needs
to connect to.

Troubleshooting:
- PegaSwitch requires use of ports 53, 80 and 8100 in order to run.
If another application is using any of those ports, or they are blocked by your 
firewall, PegaSwitch will not work.
- The ace.nro file included in the nros directory is not guaranteed to be up to date
or even to work. Please always build the latest ace.nro file from libtransistor.

Things to expect:
- Once you exit PegaSwitch on your console, the console will probably crash. This
is normal.
- You will also see an error when you reboot about your mii database being corrupted.
This is also normal. Yes, all of your miis have been deleted too.

## Libtransistor

Libtransistor is the low-level library to access the switch functionality.
Basically an unofficial version of the Nintendo SDK. Libtransistor relies on
the clang5 compiler (instead of gcc), which should be massively easier to setup.
You must use clang version 5, libtransistor will not work with any earlier versions.

To start with, you'll need to install a collection of base development tools.
You can do that with `sudo apt-get install build-essential` on Ubuntu/Debian, or
`sudo pacman -Syu base-devel` on ArchLinux.

Next, we'll need to install llvm/clang5.

- For ArchLinux, just run `sudo pacman -Syu clang`, and you'll get the right
version.

- For Ubuntu/Debian, you'll need to add the LLVM repository into `/etc/apt/sources.list`.
You'll need to find the repositories that match your OS version on the
[LLVM website](https://apt.llvm.org/). For instance for Ubuntu Xenial (16.04),
you'd add the following to your sources.list file :

```
deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial main
deb-src http://apt.llvm.org/xenial/ llvm-toolchain-xenial main
# 4.0
deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-4.0 main
deb-src http://apt.llvm.org/xenial/ llvm-toolchain-xenial-4.0 main
# 5.0
deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main
deb-src http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main
```

You'll then want to run `sudo apt-get install clang-5.0` to get `clang5`
installed.

With this done, you'll need to actually clone and build libtransistor.

```
git clone --recursive https://github.com/reswitched/libtransistor
cd libtransistor
# For archlinux
make
# For ubuntu/debian
make LLVM_POSTFIX=-5.0
```

A small note on the ubuntu/debian users : Each time I mention `make` to compile
an NRO, you will need to set `LLVM_POSTFIX=-5.0` afterwards. Otherwise, it will
use the wrong version and clang, and will probably result in compile errors.

This will compile `libtransistor`, along with a bunch of supporting libraries
(`newlib`, `compiler-rt`, `libssp`, ...). If all went well, it should have
created a folder in `build/tests` with a bunch of NROs you can load. Those are
your first homebrews !

To start them, connect your switch to pegaswitch, and type
`runnro path/to/nro.nro` in the pegaswitch console. If it doesn't crash your
switch, it should run !

You should probably set the `LIBTRANSISTOR_HOME` environment variable to your
`libtransistor` folder, as this is how `make` will find where libtransistor is.
You can do that by writing `export LIBTRANSISTOR_HOME=/path/to/libtransistor` in
your shell's RC file (`~/.bashrc` for instance).

## Ace Loader

Ace Loader is the first "Homebrew" that you should launch on your switch. It
has three jobs : 

- Clean up the browser and everything else so your Homebrew gets a clean
environment to run in
- Set up stdio redirections to a TCP server, so you can get some debug output.
- Create a server on which you can push NROs to load, or run some simple
commands.

To compile it, go back into your libtransistor folder, and go into
`projects/ace_loader` and run `make` in there. This will generate an
`ace.nro` file that you can load with pegaswitch.

If you want to get stdout from a homebrew application, you should run the command
`nc -v -l -p 2991` in another terminal BEFORE loading ace.nro. When ace.nro first
starts, it will attempt to connect to the PC running PegaSwitch on port 2991 in 
order to send all output via the network. Once ace.nro has finished loading, you
will see your Switch's ip address in the log.

To run other NROs afterward, you'll need to connect on your switch IP, port
`2991`. You can use the following command to run the helloworld example :
`ncat --send-only switchip 2991 < build/tests/test_helloworld.nro`.

Troubleshooting:

- Command ncat / nc not found? 
Try installing nmap. 
`sudo apt-get install nmap` on Ubuntu/Debian, or
`sudo pacman -Syu nmap` on ArchLinux.

- I'm not getting any output from the switch when I run `nc -v -l -p 2991`?
Make sure port 2991 isn't blocked on any firewalls.
Stdout in this way is only supported if you load nro files through ace_loader / 
ace.nro. If you built another nro file and loaded it directly from PegaSwitch
then you won't see any output.
Make sure you have built the latest version of ace_loader from inside libtransistor.
The version of ace.nro that comes with PegaSwitch may be old.

## RetroArch and Snes9x-2010

Credit to Mission2000 for these ports.

Disclaimer: The instructions in this section relate to projects that are under
active development. These instructions will probably become out of date quickly.

Limitations:

- The snes rom is currently compiled inside the nro file. Therefore you must compile 
a new copy of the emulator for each and every rom you want to play.
- Input / controls are still under development. They may work well, or not at all. 
This is NOT a bug.
- You will probably need to reboot the console to quit the game / emulator.

As of 2017/12/29, there is no graphics implemented into libtransistor. In order to 
compile RetroArch, you will first need to get the 
[graphics-experimental-fs](https://github.com/reswitched/libtransistor/tree/graphics-experimental-fs) branch of libtransistor and compile it. If you already have libtransistor checked out, you can simply `git checkout 
origin/graphics-experimental-fs`. Or if you would rather checkout just the specific 
branch, you can use `git clone 
--recursive -b graphics-experimental-fs https://github.com/reswitched/libtransistor.git`. 
Once you have the branch checked out, you can run make.

Troubleshooting:
- I'm getting an error about `implicit declaration of function 'closedir'` or `<dirent.h> 
not supported` or `unknown type name 'DIR'`? See the section below about updating submodules.
- I'm getting an error about `libtransistor/sdl2/configure: not found` or `libtransistor/build
/sdl2/Makefile' failed`? The SDL2 submodule hasn't been updated properly. See the section 
below about updating submodules.

Updating Submodules
The graphics-experimental-fs branch of libtransistor uses a different revision of the newlib 
submodule, which includes a working dirent.h header. Run `git submodule update`. If that 
doesnt work, try `git submodule update --init --recursive`. If that still hasn't properly 
updated the submodules then you may need to try just checking out the specific branch into 
a new directory: `git clone --recursive -b graphics-experimental-fs 
https://github.com/reswitched/libtransistor.git`.

Once you have built the graphics-experimental-fs branch of libtransistor, you can now move 
on to Snes9x. Checkout [libtransistor-snes9x2010](https://github.com/reswitched/libtransistor-snes9x2010)
and make it as follows:

```
git clone https://github.com/reswitched/libtransistor-snes9x2010.git
cd libtransistor-snes9x2010
make platform=switch LIBTRANSISTOR_HOME=/path/to/libtransistor/graphics/branch
```
Depending on whether you already set an environment variable for LIBTRANSISTOR_HOME, you 
may need to put the path in to the make command as well. Ensure that the path is to the 
graphics-experimental-fs branch that you have just built.

When it has successfully finished building, you will have a file called `snes9x2010_libretro_switch.a`
in your libtransistor-snes9x2010 folder.

Next up is building [libtransistor-retroarch](https://github.com/reswitched/libtransistor-retroarch)

```
git clone https://github.com/reswitched/libtransistor-retroarch
cd libtransistor-retroarch

# Create a new folder called fs
mkdir fs

# Move the snes9x2010_libretro_switch.a file we built before into the libtransistor-retroarch 
# folder and rename it to libretro_switch.a
mv /path/to/libtransistor-snes9x2010/snes9x2010_libretro_switch.a ./libretro_switch.a
```

You are just about ready to go, but first you need to find a single snes rom file (no, we 
won't tell you where to get them, do not ask) and copy it into the fs folder that we just created.
Once the rom file is in the fs folder, rename it to be called `what`. Yes, thats right, just `what`, 
with no extension.

Now you are ready to make it: `make -f Makefile.switch LIBTRANSISTOR_HOME=/path/to/libtransistor/graphics/branch`

You can now take the resulting `retroarch_switch.nro` file and load it via PegaSwitch and ace_loader.

If you decide you want to rebuild it to try a different rom, be sure to delete both the `retroarch_switch.nro` 
file as well as the `fs.squashfs` files before rebuilding.

Troubleshooting:
- I'm getting an error `ld.lld-5.0: error: libretro_switch.a(libretro.o) is incompatible with version_git.o
Makefile.switch:57: recipe for target 'retroarch_switch.nro.so' failed`?
This means that you probably didn't build `libtransistor-snes9x2010` properly. Go back and ensure you
build it with the correct platform. Then re-copy the `libretro_switch.a` file into the `libtransistor-retroarch`
folder.
- I'm getting an error `No rule to make target 'libretro_switch.a', needed by 'retroarch_switch.nro.so'.  Stop.`?
This happens when you are missing the `libretro_switch.a` file from the `libtransistor-retroarch` folder.
- I'm getting the error `[ERROR] Could not read content file "what".` when I run it with PegaSwitch?
This happens when the rom file hasn't been properly attached. Make sure that your rom file is named `what` in the
fs directory. Delete both the `retroarch_switch.nro` file as well as the `fs.squashfs` files before rebuilding.

## Where to go from here:

With this, you have a fully working development environment. You can compile and
run NROsand you should also be able to run Snes9x!

But most importantly, you can help us build awesome stuff for the Switch. If you
are willing to give us a helping hand, don't hesitate to join our
[Discord](https://discordapp.com/invite/DThbZ7z).

### Last Updated: 2017/12/29

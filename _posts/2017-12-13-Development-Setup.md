---
layout: post
category
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

## Libtransistor

Libtransistor is the low-level library to access the switch functionality.
Basically an unofficial version of the Nintendo SDK. Libtransistor relies on
the clang5 compiler (instead of gcc), which should be massively easier to setup.

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
`ace_loader.nro` file that you can load with pegaswitch.

To run other NROs afterward, you'll need to connect on your switch IP, port
`2991`. You can use the following command to run the helloworld example :
`ncat --send-only switchip 2991 < build/tests/test_helloworld.nro`.

## Where to go from here:

With this, you have a fully working development environment. You can compile and
run NROs. You could use this knowledge to run
[the SNES emulator](https://github.com/reswitched/libtransistor-snes9x2010)
on your switch !

But most importantly, you can help us build awesome stuff for the Switch. If you
are willing to give us a helping hand, don't hesitate to join our
[Discord](https://discordapp.com/invite/DThbZ7z).

### Last Updated: 2017/12/29

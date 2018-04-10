---
layout: post
category: tutorial
title: Development Environment Setup
---

In this article, we'll look at what it takes to set up a development environment
for the nintendo switch. The steps here describe the (un)officially supported
way to build Homebrew.

You will need a supported OS (ArchLinux, Debian/Ubuntu, MacOS, or Windows 10
build 17046+), and a Switch with the 3.0.0 firmware.

This guide also expects the user to be comfortable with a terminal. If you do
not know the basics of the terminal (bash, ls, cd, git...), you might want to go
look for a tutorial online first.

## Prerequiste

Some OSes will require some tools to be installed before continuing on:

- MacOS users will need to install [Homebrew](https://brew.sh/), a package
  manager. We'll be using this to cleanly install all the other tools.
- Windows 10 users will need to install the Windows Subsystem for Linux. You can
  check [Microsoft's Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
  Note that only the Ubuntu WSL is tested. From here on, Windows users can
  follow the same rules as Ubuntu, typing the commands in the WSL bash.

Finally, we'll want to install git, as that's what we'll use to download the
Reswitched tools.

- MacOS: `brew install git`
- ArchLinux: `sudo pacman -Syu git`
- Ubuntu/Debian: `sudo apt-get install git`


## Libtransistor

Libtransistor is the low-level library to access the switch functionality.
Basically an unofficial version of the Nintendo SDK. Libtransistor relies on
the clang5 compiler (instead of gcc), which should be massively easier to setup.
You must use clang version 5, libtransistor will not work with any earlier versions.

### Dealing with the deps

To start with, you'll need to install a collection of base development tools,
along with llvm5/clang5, python3 and cmake.

- For MacOS, run `brew install python3 cmake llvm`.

  For compatibility reasons, llvm is installed under `/usr/local/opt/llvm` to
  avoid conflicting with the rest of the system. You should add that to your PATH :
  `echo 'export PATH="/usr/local/opt/llvm/bin:$PATH"' >> ~/.bash_profile`.

- For ArchLinux, install one of the AUR packages (libtransistor-bin or libtransistor-git) or  simply run `sudo pacman -Syu base-devel python python-pip cmake clang lld`

- For Ubuntu/Debian, you'll need to add the LLVM repository into
  `/etc/apt/sources.list`. You'll need to find the repositories that match your
  OS version on the [LLVM website](https://apt.llvm.org/). For instance for
  Ubuntu Xenial (16.04), you'd add the following to your sources.list file :

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

  You should also fetch the LLVM signature key :

  ```
  wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
  # Fingerprint: 6084 F3CF 814B 57C1 CF12 EFD5 15CF 4D18 AF4F 7421
  ```

  And finally, install all the softwares :

  ```
  sudo apt-get update
  sudo apt-get install build-essential automake autoconf python3-setuptools squashfs-tools python3 python3-dev python3-pip cmake clang-5.0 lld-5.0
  ```

### Installing libtransistor

The recommended way to install install libtransistor is through the  binary distibutions. If you have a need to be on the unstable branch. Then continue down to "Building libtransistor itself".
For Arch the simplest thing to do is install [libtransistor-bin](https://AUR.archlinux.org/packages/libtransistor-bin/) from the AUR.
For every other distribution, follow the rest of the instructions.
First you need to obtain a copy of libtransistor. The easiest way to that is go to [libtransistor releases](https://github.com/reswitched/libtransistor/releases) and download the most recent version. For example
```wget https://github.com/reswitched/libtransistor/releases/download/vXXX/libtransistor_vXXX.tar.gz```. Replace XXX(both) with whatever the most recent version is.
```
cd path/to/the/download/location
sudo mkdir -p /opt/libtransistor
sudo tar -C /opt/libtransistor -xvzf libtransistor_vXXX.tar.gz ./
```
You should probably set the `LIBTRANSISTOR_HOME` environment variable to your
`libtransistor` folder, as this is how `make` will find where libtransistor is.
You can do that by writing `export LIBTRANSISTOR_HOME=/path/to/libtransistor/dist` in
your shell's RC file (`~/.bashrc` for instance). The AUR packages put it in `/etc/profile.d/libtransistor.sh`.

### Building libtransistor itself

With the dependencies out of the way, you'll need to actually clone and build
libtransistor.

```
git clone --recursive https://github.com/reswitched/libtransistor
cd libtransistor
# Install the python dependencies. On Arch Linux
pip install -r requirements.txt
# On everything else
pip3 install -r requirements.txt
# Build libtransistor. For MacOS and Arch Linux
make
# For Ubuntu/Debian
make LLVM_POSTFIX=-5.0
```

A small note on the Ubuntu/Debian users : Each time I mention `make` to compile
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
You can do that by writing `export LIBTRANSISTOR_HOME=/path/to/libtransistor/dist` in
your shell's RC file (`~/.bashrc` for instance).


## Where to go from here:
Optionaly set  up [Pegaswitch](https://reswitchedweekly.github.io/Pegaswitch/).
With this, you have a fully working development environment. You can compile and
run NROs and you should also be able to build and run

[RetroArch and Snes9x](https://reswitchedweekly.github.io/Building-RetroArch/)!

But most importantly, you can help us build awesome stuff for the Switch. If you
are willing to give us a helping hand, don't hesitate to join our
[Discord](https://discordapp.com/invite/DThbZ7z).

### Last Updated: 2018/04/09

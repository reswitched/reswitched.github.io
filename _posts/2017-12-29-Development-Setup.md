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

## PegaSwitch

The first thing you'll need is the tools to exploit vulnerabilities on the
Switch. For this, we use PegaSwitch, an exploit framework. To install
PegaSwitch, you need at version version 8.x of Node.JS.

- For MacOS, simply use brew: `brew install node`
- For other platforms, you can follow the tutorial on the
  [Node.JS website](https://nodejs.org/en/download/package-manager/).

You will also need to install the base development tools package for your OS,
as they are necessary to build some of the PegaSwitch dependencies:

- For ArchLinux: `sudo pacman -Syu base-devel`
- For Ubuntu/Debian: `sudo apt-get install build-essential`

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
- PegaSwitch requires use of UDP port 53 and TCP ports 80 and 8100 in order to run.
If another application is using any of those ports, or they are blocked by your 
firewall, PegaSwitch will not work. 
- The ace.nro file included in the nros directory is not guaranteed to be up to date
or even to work. Please always build the latest ace.nro file from libtransistor.
- My Switch forces me to update before starting the browser !

  To fix this, you need to restart your switch in Recovery Mode/Maintenance Mode.
  Doing so will make your switch forget there is an existing update. To reboot
  in this mode, power off your switch completely (press power multiple seconds,
  and press "Power options" -> "Power off"). Then, hold Volume Down/Volume Up
  buttons, and press power **while keeping those buttons held**. Once in
  Recovery mode, just press power to restart your switch, and try connecting
  to Pegaswitch again.

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

### Dealing with the deps

To start with, you'll need to install a collection of base development tools,
along with llvm5/clang5, python3 and cmake.

- For MacOS, run `brew install python3 cmake llvm`.

  For compatibility reasons, llvm is installed under `/usr/local/opt/llvm` to
  avoid conflicting with the rest of the system. You should add that to your PATH :
  `echo 'export PATH="/usr/local/opt/llvm/bin:$PATH"' >> ~/.bash_profile`.

- For ArchLinux, simply run `sudo pacman -Syu base-devel python python-pip cmake clang lld`

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
  sudo apt-get install build-essential python3 python3-pip cmake clang-5.0 lld-5.0
  ```

### Building libtransistor itself

With the dependencies out of the way, you'll need to actually clone and build
libtransistor.

```
git clone --recursive https://github.com/reswitched/libtransistor
cd libtransistor
# Install the python dependencies. On ArchLinux
pip install -r requirements.txt
# On everything else
pip3 install -r requirements.txt
# Build libtransistor. For MacOS and ArchLinux
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

  Make sure TCP port 2991 isn't blocked on any firewalls.
  Stdout in this way is only supported if you load nro files through `ace_loader`.

  If you built another nro file and loaded it directly from PegaSwitch then you
  won't see any output. Make sure you have built the latest version of
  `ace_loader` from inside libtransistor. The version of ace.nro that comes with
  PegaSwitch may be old.

## Where to go from here:

With this, you have a fully working development environment. You can compile and
run NROs and you should also be able to build and run 
[RetroArch and Snes9x](https://reswitchedweekly.github.io/Building-RetroArch/)!

But most importantly, you can help us build awesome stuff for the Switch. If you
are willing to give us a helping hand, don't hesitate to join our
[Discord](https://discordapp.com/invite/DThbZ7z).

### Last Updated: 2018/01/19

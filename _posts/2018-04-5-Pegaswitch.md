
---
layout: post
category: tutorial
title: Pegaswitch Setup
---

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

## Ace Loader

Ace Loader is the first "Homebrew" that you should launch on your switch. It
has three jobs :

- Clean up the browser and everything else so your Homebrew gets a clean
environment to run in
- Set up stdio redirections to a TCP server, so you can get some debug output.
- Create a server on which you can push NROs to load, or run some simple
commands.

To get Ace Loader download [libtransistor releases](https://github.com/reswitched/libtransistor/releases) and dowload wk_ace.nro.  Put it in the pegaswitch directory. In pegaswitch run `runnro wk_ace.nro`.

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

### Last Updated: 2018/04/09
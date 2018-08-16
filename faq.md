---
layout: page
title: Frequently Asked Questions
permalink: /faq/
---

This page contains the answers to some *very* frequently asked questions. Is your question not answered here? Ask on our <a href="{{ site.baseurl }}/discord">Discord</a>!

## Will ReSwitched help me get free games?

No. ReSwitched does **NOT** endorse piracy in any way, shape, or form. Our goal is to provide the ability to run homebrew, not pirate paid content.

## How can I hack my Switch?

One of our team members, @Plailect, maintains an easy-to-use Switch hacking guide at [switch.hacks.guide](https://switch.hacks.guide/).

## What firmware is best? Should I upgrade to a specific firmware?

The general rule is: **Lower is better.** It is **NOT** recommended to upgrade to any higher firmware at this time. On firmware versions up to 4.1.0, we currently have means of triggering fully privileged code execution through softwarehax. Switches vulnerable to fusée-gelée/[shofel2](https://github.com/fail0verflow/shofel2) can be hacked via RCM mode regardless of firmware version. As of 2018-07-10 there are [reports of Switches not vulnerable to fusée-gelée/shofel2](https://twitter.com/SciresM/status/1016724847504736256).

## Will ReSwitched ever release "coldboot" exploits for the Switch?

All of our current hax require user interaction; that is, they are not "coldboot". In the long term, firmware 1.0.0 is most likely to get a solution where you boot into softwarehax immediately after turning the device on. On firmware versions <3.0.2, there a theoretical vector for user interaction-less softwarehax, but it is almost impossible to use and has no accompanying savegame exploit. On firmware versions above that, it is extremely unlikely "coldboothax" will be achieved. See [this post](https://i.imgur.com/aeh6OAa.png) by @SciresM for more information.

## Will I get banned if I run hacks/custom firmware/etc?

The Switch provides extremely detailed telemetry to Nintendo. In particular, crashes and their requisite error codes are uploaded to Nintendo; lots of homebrew use custom error codes when crashing, and these being uploaded to Nintendo could definitely get you banned. If you are an end user who cares about online access, it is not recommended to run custom firmware at this time. The Switch's telemetry has not been entirely disabled even though the Error Collection sysmodule is not launched on currently available custom firmwares.

## Does ReSwitched accept donations?

ReSwitched is **NOT** accepting donations at this time. Anyone claiming otherwise is an impersonator/fraud and should be reported to us on our <a href="{{ site.baseurl }}/discord">Discord</a>.

## Will we ever get flashcarts a la the R4/Acekard/etc. on DS/3DS?

This is extremely unlikely due to a very secure cryptographic design for the carts and cart controller on the Switch. 

## Will <popular exploit in the news, e.g. rowhammer, DirtyCOW, Spectre, Meltdown, etc.> work on the Switch?

While there's no immediate way to guarantee yes or no, if said exploit *does* work on the Switch, it's likely you'll hear about it very quickly, as many groups and individuals are sure to test it on the Switch as soon as they hear about it. Given this, if you haven't heard anything about it working, it's unlikely it does.

## Questions about Nintendo Switch Internals 

Adapted from the now-defunct #vvv-faq channel on our <a href="{{ site.baseurl }}/discord">Discord</a>, thanks to @sirocyl for writing this portion of the FAQ!

### The Switch seems to have a lot of different boot modes such as RCM, safe mode, maintenance/recovery mode, etc. What do these do and how do I know if I'm in one of them?

1. **RCM**: The Tegra X1's boot recovery mode.
   1. The Switch will boot into this mode automatically if it is missing its eMMC board or has corrupted boot contents. 
   1. This mode can be triggered manually by grounding pin 10 on the right JoyCon rail, then holding `Volume Up` + `HOME` + `POWER`. More information is available [here](https://xghostboyx.github.io/RCM-Guide).
   1. The Switch's screen does not turn on, and if plugged into a computer will identify itself as "APX".
   1. Enables recovering a Switch or other Tegra device from a hard brick, as long as a USB connection can be made to a computer.
   1. A bootrom exploit for the Tegra X1, fusée-gelée/[shofel2](https://github.com/fail0verflow/shofel2), takes advantage of a security flaw in this mode.

1. **Safe Mode**: Available since firmware 4.0.0, this mode attempts to check for and download/install a System Update.
   1. Initiated by the key sequence: `Volume Down` + `POWER`, shift `Volume Down` to `Volume Up`, release `POWER`.
   1. Displays a spinner block, and a progress bar.
   1. If there is an internet connection available, it will connect and download an update.
   1. If there is an update downloaded/pending, it will install the update.

1. **Maintenance Mode**: ("Recovery Mode" in some regions/language settings). Shows the usual menu with options to reset user data on boot.
   1. Initiated by key sequence: `Volume Up` + `Volume Down` + `POWER`.
   1. Displays a menu onscreen, with choices to update system, and initialize console/restore factory settings with or without deleting save data.
   1. If there is pending update data already downloaded, launching Maintenance Mode will delete it.

1. **Normal boot**: Normal boot into the Switch operating system.
   1. Initiated by pressing `POWER` with the system off.
   1. Boots normally, displaying the stock "Nintendo Switch" boot logo.
   1. Loads qlaunch/Home Menu and all regular services as usual.

### There's a lot of jargon thrown around such as "ROP, ACE, Horizon, Userland, Kernel, Hypervisor, TrustZone, EL0, EL1, EL2, EL3, etc." What do all these terms mean?

1. **ROP**: A non-functional form of code execution used to bootstrap further exploitation. PegaSwitch uses ROP to pop into ACE.
1. **ACE**: Arbitrary Code Execution. This is the "holy grail" of homebrew, and allows one to write programs which run on the Switch.
1. **Horizon/NX** (aka **HOS**): The Switch operating system. It is derived from the OS on the Nintendo 3DS, Horizon/CTR, with extensive changes and modernization throughout. It is **not** FreeBSD-based, or based on any known OS/RTOS kernel; it is entirely custom.
1. **Userland (EL0)**: Where regular applications on the Switch live. They are stripped of all but the most essential privileges, and may be limited in terms of hardware access and capabilities.
1. **Kernel (EL1)**: The core component of Horizon, responsible for the vast majority of system-level tasks. Achieving kernel access allows for a greatly-expanded set of capabilities for homebrew development, system modification and development capabilities, such as launching custom firmware, and patching of system binaries and applications to change their behaviors.
1. **Hypervisor (EL2)**: An execution level between Kernel and TrustZone allowing for virtualization of the underlying OS. Unused on the Switch.
1. **TrustZone (EL3)**: A new concept in the ARM architecture that Nintendo is using for the first time on the Switch. On the Switch, the TrustZone, through "Secure Monitor calls" (SMCs), performs crypto, and a small number of system tasks like power management and sleep. See [here](https://www.arm.com/products/security-on-arm/trustzone) for more information. 
   1. TrustZone access is necessary to dump one's own keys for off-system crypto, and to bootstrap a custom hypervisor in "EL2". 

### Is there a way to bypass the fuse burned on major system firmware updates, allowing downgrading the Switch firmware to more vulnerable versions?

The fuses in the Nintendo Switch are embedded into the SoC, and thus are not feasibly bypassable via any hardware modification. Fuse checks can be bypassed with a bootrom-level exploit like fusée-gelée/[shofel2](https://github.com/fail0verflow/shofel2), but downgrading is not particularly useful for the end user at that point since you've already achieved the most privileged level of execution possible. Additionally, if you downgrade through a method like this, you will be reliant on that method to boot until you upgrade again, since normal boot will be interrupted by the failing fuse checks.
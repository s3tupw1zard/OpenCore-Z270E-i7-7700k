# OpenCore files for Z270E working with Intel i7-7700k

## Hardware

| Component | Model |
| ------ | ------ |
| Motherboard | Asus ROG Strix Z270E Gaming |
| CPU | Intel Core i7-7700K |
| Memory | Corsair Vengeance Pro (I'll Correct this when have time to look which RAM Model it really is) |
| Storage | Intenso 1TB M.2 SATA SSD |
| GPU | AMD Radeon R9 280X w/ 3GB VRAM |
| Wi-Fi & Bluetooth | Both Onboard - So Wi-Fi isn't working right now |

Any other relative recent AMD Graphics Card should work as far Apple hasn't dropped it, as of: [AMD GPUs](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html)

NOTE: For some components I'm not quite sure which models they actually are. I will add the models that are not specified exactly at a later date.

Software

| Component | Model |
| OpenCore | 0.8.3 |
| macOS | 12.5.1 (Big Sur works as well) |

## How to get started

Read the Dortania's OpenCore Install Guide. Set the MLB, ROM, SystemSerialNumber and SystemUUID as instructed.

## Status

I have tested **all** the features so far **except features like FileVault, Siri, printer and scanner and trackpad** and so far everything is working fine. However, hibernating doesn't work for me in that when macOS goes to sleep, it can't turn the screen back on completely. In this case, the screen turns on, but the picture remains black. For this I have quoted a fixing guide down below.

Currently everything else works as excepted.

### Current Status of things I need to do in the future:\

#### TODO:\

- [ ] Add Pictures of successful macOS installation and system information
- [ ] Fixing Memory speed in ``About this Mac`` (MHz)
- [ ] Add guide for fixing Propertree blank window on Monterey and installing to ``/Applications``
- [ ] Checking and eventually fixing Facetime, Messages etc.
- [ ] Add link to correct version of ``OpenCore Configurator``
- [ ] Add Guide how to upgrade to macOS Ventura beta (But probably only when the stable version MacOS Ventura is released.)
- [ ] Checking and testing FileVault
- [ ] Add links to useful tools i.e. for setting correct SMBIOS stuff
- [ ] Add Windows/Linux dual boot guide

## Guides for this setup:\

### Fixing Hibernation (Source: Listing 01)

I am quoting a section from ``Fixing Sleep`` from [Dortania's Universal Guides](dortania.github.io) here:

> #### Preparations
>
> ##### In macOS:\
>
> Before we get in too deep, we'll want to first ready our system:
>
>> ``sudo pmset autopoweroff 0``
>> ``sudo pmset powernap 0``
>> ``sudo pmset standby 0``
>> ``sudo pmset proximitywake 0``
>> ``sudo pmset tcpkeepalive 0``
>
>
>
> ##### In your config.plist:\
>
> While minimal changes are needed, here are the ones we care about:
> ``Misc -> Boot -> HibernateMode`` -> ``None``
> We're gonna avoid the black magic that is S4 for this guide
> ``NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> boot-args``
> ``keepsyms=1`` - **Makes sure that if a kernel panic does happen during sleep, that we get all the important bits from it**
> ``swd_panic=1`` - **Avoids issue where going to sleep results in a reboot, this should instead give us a kernel panic log**
>
> ##### In your BIOS:\
>
> Disable:
> ``Wake on LAN``
> ``Trusted Platform Module``
> **Note that if you're using BitLocker in Windows, disabling this will result in all your encryption keys being lost. If you're using BitLocker, either disable or note that it may be a cause for wake issues.**
> ``Wake on USB`` **(Certain boards may actually require this on to wake, but most will get random wakeup calls with it)**
> Enable:
> ``Wake on Bluetooth`` **(If using a Bluetooth device for waking like a keyboard, otherwise you can disable)**

#### Sources of guides etc.:\

Source Listing 01: [Fixing Sleep from dortania.github.io](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#preparations)

If anyone has additions or ideas what guides to add feel free to open a issue.

**NOTE: This repo is just intended for providing Information and, of course, the OpenCore files to get macOS running on this setup. This is not the right place for asking for help not regarding this specific setup, please use a dedicated forum for this i.e. [tonymacx86.com](https://www.tonymacx86.com). But if something is not right with the ``config.plist`` i.e. if some values don't work with a new release of macOS feel free to open a pull request for correcting such stuff. I'll then add a new, corrected release**

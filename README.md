# Hackintosh-Z490-Aorus-Master-10900K

This is a repository of my EFI folder for my Hackintosh. Details on the used hardware is listed below. The installation is completely based on OpenCore and I basically followed the excellent guide from [Dortania](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) for Comet Lake CPUs. 

## Credits

- [Acidanthera](https://github.com/acidanthera) for [OpenCore](https://github.com/acidanthera/OpenCorePkg), [WhateverGreen](https://github.com/acidanthera/WhateverGreen), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), and [Lilu](https://github.com/acidanthera/Lilu)
- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)
- [RadeonSensor](https://github.com/aluveitie/RadeonSensor) from [aluveitie](https://github.com/aluveitie)

## Hardware

- **CPU**: Intel i9 10900K
- **Mainboard**: Gigabyte Aorus Master Z490
  - 2.5Gbit Ethernet: Intel I225-V
  - Audio: Realtek ALC1220-VB (disabled)
  - WiFi / BT: Intel Wi-Fi 6 AX201 (disabled)
- **GPU**: XFX AMD Radeon RX 5700 DD Ultra
  - Flashed with XFX AMD Radeon RX 5700 XT Thicc II BIOS
- **WiFi / BT**: PCIe extension card with Broadcom BCM94360CD chip
- **Audio**: External USB DAC/AMP

## Working stuff

- Onboard ehternet via Intel I225-V
- All USB ports (properly mapped, see section below)
- AppleTV, Netflix, Amazon Prime
- Sleep/Wake
- Shutdown

## Not working

- Sidecar

## Not tested
- Onboard audio via Realtek ALC1220-VB
- Onboard WiFi / BT via Intel Wi-Fi 6 AX201

## Installation

### Pre-install steps
- Setup Bios according to [this guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings).

### Generation of installation medium
- Create boot drive according to [this guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os) (you will need access to another Mac)
- Mount the EFI of you installation medium and copy the content of this repository to the EFI folder. To easily mount the EFI, I highly recommned [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)
- You still need to edit the config.plist and create your custom PlatformInfo for **iMacPro1,1** using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). I highly recommend [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) or [ProperTree](https://github.com/corpnewt/ProperTree) to edit the config.plist.

### OS installation

-  Boot from the boot drive and install macOS to the hard drive.

### Post-install steps

- Mount the EFI of your hard drive with the macOS installation and copy the previously created EFI folder. This allows to directly boot from you hard drive.
- For proper sleep, setup sleep setting according to [this guide](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#fixing-sleep)

## Details on the installation

### USB mapping

- The USB ports of the Gigabyte Aorus Master Z490 was mapped according to [this guide](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit).
- To not exceed the 15 port limit o macOS HS06 is disabled. This means that there is no USB2.0 support for the USB3.2 Type-C port of the mainboard.
- The following image shows the port mapping of the mainboard:

- The following table shows details of the mapped ports:
- | Name | Port     | Type | Active in USBMap.kext |
|------|----------|------|-----------------------|
| HS03 | 03000000 | 0    | enabled               |
| HS04 | 04000000 | 0    | enabled               |
| HS05 | 05000000 | 0    | enabled               |
| HS06 | 06000000 | 0    | disabled              |
| HS07 | 07000000 | 0    | enabled               |
| HS08 | 08000000 | 0    | enabled               |
| HS09 | 09000000 | 0    | enabled               |
| HS11 | 0B000000 | 0    | enabled               |
| HS13 | 0D000000 | 255  | enabled               |
| SS03 | 13000000 | 3    | enabled               |
| SS04 | 14000000 | 3    | enabled               |
| SS05 | 15000000 | 3    | enabled               |
| SS06 | 16000000 | 8    | enabled               |
| SS07 | 17000000 | 3    | enabled               |
| SS08 | 18000000 | 3    | enabled               |
| SS09 | 19000000 | 3    | enabled               |

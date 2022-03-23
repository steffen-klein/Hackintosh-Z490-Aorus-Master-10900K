# Hackintosh-Z490-Aorus-Master-10900K

This is a repository of my EFI folder for my Hackintosh. Details on the used hardware is listed below. The installation is completely based on OpenCore and I basically followed the excellent guide from [Dortania](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) for Comet Lake CPUs. 

## Credits

- [Acidanthera](https://github.com/acidanthera) for [OpenCore](https://github.com/acidanthera/OpenCorePkg), [WhateverGreen](https://github.com/acidanthera/WhateverGreen), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), and [Lilu](https://github.com/acidanthera/Lilu)
- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)

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
- Compare your settings to the following screenshots:

### Generation of installation medium
- Create bootdrive according to [this guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os) (you will need access to another Mac)
- Mount the EFI of you installation medium and copy the content of this repository to the EFI folder. To easily mount the EFI, I highly recommned [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)
- You still need to edit the config.plist and create your custom PlatformInfo for **iMacPro1,1** using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). I highly recommend [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) or [ProperTree](https://github.com/corpnewt/ProperTree) to edit the config.plist.

### OS installation

### Post-install steps

## Details on the installation

### USB mapping

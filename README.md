# Hackintosh – Z490 Aorus Master – Intel 10900K – AMD 6800 XT #

This is a repository of a custom EFI which allows the installation of macOS on the Z490 Aorus Master Mainboard with the Intel 10900K CPU. Details on the used hardware are listed below. The installation is completely based on OpenCore and I basically followed the excellent guide from [Dortania](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) for Comet Lake CPUs.

The current guide was tested with OpenCore 0.85 and macOS Venture 13.0

## Credits ##

- [Acidanthera](https://github.com/acidanthera) for [OpenCore](https://github.com/acidanthera/OpenCorePkg), [Lilu](https://github.com/acidanthera/Lilu), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), [WhateverGreen](https://github.com/acidanthera/WhateverGreen), and [NVMeFix](https://github.com/acidanthera/NVMeFix)
- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)
- [RadeonSensor](https://github.com/aluveitie/RadeonSensor) from [aluveitie](https://github.com/aluveitie)
- [ProperTree](https://github.com/corpnewt/ProperTree)

## Hardware ##

- **Mainboard**: Gigabyte Aorus Master Z490
  - 2.5Gbit Ethernet: Intel I225-V
  - Audio: Realtek ALC1220-VB (disabled)
  - WiFi / BT: Intel Wi-Fi 6 AX201 (disabled)
- **CPU**: Intel i9 10900K
- **RAM**: Corsair Vengeance LPX 32GB (2 x 16GB) DDR4 3200MHz C16
- **GPU**: AMD Radeon™ RX 6800 XT Graphics
- **WiFi / BT**: PCIe extension card with Broadcom BCM94360CD chip
- **Audio**: External USB DAC/AMP - Schiit Modius & Schiit Asgard
- **Storage**: WD_BLACK SN750 NVMe SSD 2 TB
- **PSU**: BeQuiet! Dark Power 12 1000W

## Working stuff ##

- Onboard ethernet via Intel I225-V ([custom firmware needs to be flashed](https://github.com/5T33Z0/Gigabyte-Z490-Vision-G-Hackintosh-OpenCore/blob/main/I225-V_FIX.md#option-2-flashing-a-custom-firmware))
- All USB ports (properly mapped, see section below)
- AppleTV, Netflix, Amazon Prime
- Sleep/Wake
- Shutdown

## Not working ##

- Sidecar
- Onboard WiFi / BT via Intel Wi-Fi 6 AX201

## Not tested ##
- Onboard audio via Realtek ALC1220-VB

## Installation ##

### Pre-install steps ###
First, I highly recommend to update the BIOS to the latest version. In this guide, I am using Version 21 of the Gigabyte Aorus Master Z490.

Next, setup Bios according to [this guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#intel-bios-settings). In the following the relevant settings are listed. You can also find a BIOS settings file under Z490-AORUS-MASTER-BIOS-V21-SETTINGS and screenshots of all BIOS settings.

#### Tweaker – Advanced CPU settings  ####
- **VT-d**: Enabled

#### Settings – IO Ports ####
- **Internal Graphics**: Enabled
- **DVMT Pre-Allocated**: 64MB
- **DVMT Total Gfx Mem**: MAX
- **Aperture Size**: 256MB
- **OnBoard LAN Controller**: Enabled
- **Audio Controller**: Disabled
- **Above 4G Deconding**: Enabled
- **Re-Size BAR Support**: Auto

#### Settings – IO Ports - USB Configuration ####
- **Legacy USB Support**: Disabled
- **XHCI Hand-off**: Enabled

#### Settings – Miscellaneous ####
- **Intel Platform Trust Technology(PTT)**: Enabled
- **Software Guard Extensions(SGX)**: Disabled

#### Settings – Miscellaneous – Trusted Computing ####
- **Security Device Suppert**: Enabled

#### Boot ####
- **Fast Boot**: Disable Link
- **Windows 10 Features**: Windows 10 WHQL
- **CSM Support**: Disabled

#### Boot - Secure Boot ####
- **Secure Boot Enable**: Disabled

### Generation of installation medium ###
- Create an installation medium according to [this guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os) (you will need access to another Mac)
- Mount the EFI partition of the installation medium and copy the content of this repository to the EFI partition. To easily mount the EFI partition, I highly recommned [MountEFI](https://github.com/corpnewt/MountEFI) from [corpnewt](https://github.com/corpnewt)
- You still need to edit the config.plist and create your custom PlatformInfo for **iMacPro1,1** using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). I highly recommend [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) or [ProperTree](https://github.com/corpnewt/ProperTree) to edit the config.plist.

### OS installation ###

-  Boot from the installation medium and install macOS to the SSD.

### Post-install steps ###

- Mount the EFI partition of your SSD and copy the previously created EFI folder. This allows to directly boot from your SSD.
- For proper sleep, setup sleep setting according to [this guide](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#fixing-sleep)

## Quirks ##

### USB mapping ###

- The USB ports of the Gigabyte Aorus Master Z490 were mapped according to [this guide](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit).
- To not exceed the 15 port limit of macOS HS06 is disabled. This means that there is no USB2.0 support for the USB3.2 Type-C port of the mainboard.
- The following table shows details of the mapped ports:

| Name | Port     | Type | Active in USBMap.kext |
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

- The following image shows the port mapping of the mainboard:

![UBS Mapping for Z490 Aorus Master](USB%20Mapping%20for%20Z490%20Aorus%20Master.png?raw=true "Title")

### i9 10900k undervolting ###
To reduce the power draw of the CPU and achieve a more silent operation, I applied the following BIOS settings:

#### Tweaker ####

- **CPU Clock Ration**: 53
- **Extreme Memory Profile(X.M.P.)**: Profile1
- **CPU Vcore**: Normal
- **Dynamic Vcore(DVID)**: -0.065V (Need to be manually optimized in small steps)

#### Tweaker – Advanced CPU Settings ####

 - **Active Turbo Ratios**: Enabled
   - **Turbo Ratio (1-Core Active)**: 53
   - **Turbo Ratio (2-Core Active)**: 53
   - **Turbo Ratio (3-Core Active)**: 52
   - **Turbo Ratio (4-Core Active)**: 52
   - **Turbo Ratio (5-Core Active)**: 51
   - **Turbo Ratio (6-Core Active)**: 51
   - **Turbo Ratio (7-Core Active)**: 50
   - **Turbo Ratio (8-Core Active)**: 50
   - **Turbo Ratio (9-Core Active)**: 49
   - **Turbo Ratio (10-Core Active)**: 49
 - **Turbo Power Limits**: Enabled
    - **Package Power Limit1 - TDP (Watts)**: 180
    - **Package Power Limit2 (Watts)**: 180

#### Settings – Smart Fan 5 ####
To reduce the operation noise of the system, I applied a custom fan curve to all fans in the system:

![Smart FAN 5](./BIOS/Screenshots/20_Settings_Smart-Fan-5.png?raw=true "Title")

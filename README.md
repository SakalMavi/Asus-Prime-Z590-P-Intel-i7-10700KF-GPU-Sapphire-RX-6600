# Asus-Prime-Z590-P-Intel-i7-10700KF-GPU-Sapphire-RX-6600
Asus Prime Z590-P Intel i7-10700KF GPU Sapphire RX 6600 Pulse Opencore 1.0.3 - MacOS Sequoia 15.2

Install macOS Sequoia on ASUS PRIME Z590-P Gaming Mainboard with 10th Gen Intel CPU.

![image](https://github.com/user-attachments/assets/e09e04b7-6515-4cec-9c47-11af18f6ca8c)

### Information

This Hackintosh was created with help of some motivating projects like [SchmockLord/Gigabyte-Z590i-Vision-D-11900k](https://github.com/SchmockLord/Gigabyte-Z590i-Vision-D-11900k) and the OpenCore guide [Desktop Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) as base.

- macOS: [Monterey 12.7.6](https://support.apple.com/en-us/HT212585)
- bootloader: [OpenCore 1.0.1](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.1)
  - [Configuration](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf) and [Differences](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Differences/Differences.pdf)

<a href="https://www.buymeacoffee.com/rafaelmaeuer"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=☕️&slug=rafaelmaeuer&button_colour=F2F2F2&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=FFDD00"></a>

---

**Table of Contents**

- [ASUS PRIME Z590-P Hackintosh](#asus-prime-z590-p-hackintosh)
  - [Information](#information)
    - [Hardware](#hardware)
    - [Performance](#performance)
  - [Install macOS](#install-macos)
    - [1. Installer-Drive](#1-installer-drive)
    - [2. BIOS Settings](#2-bios-settings)
    - [3. Install macOS](#3-install-macos)
    - [4. Post Install](#4-post-install)
  - [Update macOS](#update-macos)
  - [DualBoot Windows](#dualboot-windows)
  - [Resources](#resources)
    - [Boot Flags](#boot-flags)
    - [ACPI Patches](#acpi-patches)
    - [Kexts](#kexts)
    - [Tools](#tools)
    - [Troubleshooting](#troubleshooting)
  - [Credits and Documentation](#credits-and-documentation)

---

#### Hardware

| Component    | Variant                                                           | Info                                                                                                                                                                                                                                                                                                           | 
| ------------ | ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | 
| Mainboard    | ASUS PRIME Z590-P                                                 | (https://www.asus.com/Motherboards-Components/Motherboards/PRIME/PRIME-Z590-P-CSM/)                                                                                                                                                                                                                            | 
| Processor    | Intel Core i7 10700KF                                             | (https://ark.intel.com/content/www/us/en/ark/products/199325/intel-core-i710700kf-processor-16m-cache-up-to-5-00-ghz.html)                                                                                                                                                                                     | 
| DDR4 RAM     | Crosair Vengeancea-lpx 32GB                                       | (https://www.corsair.com/us/en/p/memory/cmk16gx4m2b3200c16/vengeancea-lpx-16gb-2-x-8gb-ddr4-dram-3200mhz-c16-memory-kit-black-cmk16gx4m2b3200c16?srsltid=AfmBOoplsIjQP4F38BSt8KVhaFCW                                                                                                                          [
| NVMe SSD     | Samsung 980 Pro 1TB                                               | (https://www.samsung.com/us/computing/memory-storage/solid-state-drives/980-pro-pcie-4-0-nvme-ssd-1tb-mz-v8p1t0b-am/)                                                                                                                                                                                          | 
| Graphics     | Sapphire RX 6600 Plus 8GB                                         | (https://www.sapphiretech.com/en/consumer/11310_05_20g-radeon-rx-6600-8g-gddr6)                                                                                                                                                                                                                                | 


---

#### 2. BIOS Settings

- Update to version 1601 (firmware in [BIOS](/BIOS) folder)
- Use following BIOS settings (DEL/F2 on boot):

  EZ-Mode
  
  ```sh
  EZ System Tuning
    - ASUS Extreme Tuning
  ```

  Advanced Mode (F7)

  ```sh
  Ai Tweaker
    - Ai Overclock Tuner: XMP I
  Advanced
    - CPU Configuration
      - Intel (VMX) Virtualization Technology: Enabled
    - System Agent (SA)-Configuration
      - Graphics Configuration
        - iGPU Multi-Monitor: Disabled
    - PCH Storage Configuration
      - SATA6G_(1-4) Hot Plug: Enabled
    - Thunderbolt(TM) Configuration
      - Discrete Thunderbolt(TM) Support: Disabled
    - PCI Subsystem Settings
      - Above 4G Decoding: Enabled
    - USB Configuration
      - Legacy USB Support: Enabled
      - XHCI Hand-off: Enabled
    - Onboard Devices Configuration
      - Serial Port Configuration
        - Serial Port: Disabled
  Boot
    - CSM (Compatibility Support Module)
      - Launch CSM: Disabled
    - Secure Boot
      - OS Type: Windows UEFI mode
      - Key Management
        - Clear Secure Boot Keys: Execute
    - Boot Configuration
      - Fast Boot: Disabled
      - POST Delay Time: 0 sec
      - Wait For 'F1' If Error: Disabled
  Tool
    - ASUS Armoury Crate
      - Download & Install ARMOURY CRATE app: Disabled
  ```

---

#### 3. Install macOS

- ⚠️ Connect Installer-Drive to **USB2** port ⚠️
- Boot from Installer-Drive (`F8` on BIOS post -> `[UEFI] USB Drive`)
- Select macOS Installer (`Install macOS Monterey`)
- Begin installation on APFS formatted SSD
- Finish the initial macOS setup process

---

#### 4. Post Install

**a) OpenCore**

- After successful install copy OpenCore to system EFI partition
- Repeat steps 1b + 1c but with EFI of macOS SSD as target
  - Switch OpenCore from `debug` to `release` version ([file-swaps](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html#file-swaps))
  - To disable all logging apply following [config-changes](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html#config-changes)

**b) Sleep/Wake**

- Read and follow instructions in [Docs/SLEEP](Docs/SLEEP.md).

**c) Tools**

- Install the following from [Tools](/Tools) folder:
  - `OpenCore Configurator` (OCC) to modify/update `config.plist`
  - `Hackintool` to check loaded kexts, system settings and more

**d) Security**

- Use [SilentKnight](https://eclecticlight.co/lockrattler-systhist/) to check security state and update missing software or tools.

**e) Audio**

- (Optional) AppleALC layout-id 12.

---

### Update macOS

Check the official update-guide: [OpenCore-Post-Install/update](https://dortania.github.io/OpenCore-Post-Install/universal/update.html)

1. Backup
   - Full system backup with `Time Machine` or similar software
   - Copy current EFI to OpenCore USB-Drive for recovery purpose
2. Download
   - Latest version of OpenCore and replace files in EFI
   - Updates for all installed kexts and replace in EFI
3. Reboot
   - Boot with updated OpenCore version and kexts
   - If the system doesn't boot, use OpenCore USB-Drive to roll back
4. Update
   - Start macOS Update from `System Settings` -> `Software Update`
   - With OpenCore the update process should work automatically
   - If `Software Update` shows `Mac version is up to date`, download macOS Installer from AppStore and start the update manually

If the system doesn't boot, try to fix the problem or revert to the latest EFI or system-backup.

---

### DualBoot Windows

1. Install
   - Create new partition (~106 GB min) with `disk utility`
   - Create a Windows 11 Installer with [Rufus](https://rufus.ie/) (TPM 2.0 + Secure-Boot)
   - Select `Windows` boot entry in OpenCanopy to begin installation
   - Delete the partition from installer and let Windows re-create it

2. Drivers
   - Use the `Z590-P Driver-DVD` to install all missing drivers
   - Unzip drivers in [Windows/Driver](Windows/Driver/) folder and install manually from Device-Manager (`Broadcom BT/WiFi` and `Marvel Console`)
   - For Magic Mouse scrolling install `AppleWirelessMouse64.exe` from [Windows/Mouse](Windows/Mouse/) folder

3. Fixes
   - For Scroll-Inversion follow the instructions from [windowscentral.com](https://www.windowscentral.com/how-reverse-scrolling-direction-windows-10)
   - For Keyboard remapping use [AutoHotkey](https://www.autohotkey.com/) and [SharpKeys](https://github.com/randyrants/sharpkeys) with proper config files from [Windows/Keyboard](Windows/Keyboard/) folder
   - Fix incorrect clock settings by instructions from [lifehacker.com](https://lifehacker.com/fix-incorrect-clock-settings-in-windows-when-dual-booti-5742148)
   - Currently there are two concurrent problems:
     - Don't install BT-Driver in Windows: Mouse works on both OS while restart, but no Scroll in Windows
     - Install BT-Driver in Windows: Scrolling in Windows works, but restart breaks connection for other OS

---

### Resources

Basic information to run this Hackintosh. For more detailed information see [Docs/CONFIG](Docs/CONFIG.md).

#### Boot Flags

The following bootflags are used:

- [alcid=11](https://github.com/acidanthera/AppleALC/blob/master/Resources/ALC897/Info.plist) for ALC897 audio config
- [darkwake=0](https://dortania.github.io/OpenCore-Post-Install/usb/misc/keyboard.html#method-3-configuring-darkwake) fixes `Wake by RTC/Maintenance`
- [agdpmod=pikera](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html#navi-23-series) for display out with RX 6600 XT GPU

#### ACPI Patches

Several SSDT patches are [recommended](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-prebuilt.html#desktop-comet-lake) by dortania (generated with [SSDTTime](https://github.com/corpnewt/SSDTTime)):

| Patch                   | Name               | Link                                                                                                                                |
| ----------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| Fix System Clock        | SSDT-AWAC.aml      | [dortania/acpi/awac-methods](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac-methods/prebuilt.html)             |
| Fix Embedded Controller | SSDT-EC.aml        | [dortania/acpi/ec-fix](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)                                  |
| Fix Power Management    | SSDT-PLUG.aml      | [dortania/acpi/plug](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)                                      |
| Fix USB RHUB            | SSDT-USB-Reset.aml | [dortania/acpi/rhub-methods](https://dortania.github.io/Getting-Started-With-ACPI/Universal/rhub-methods/ssdttime.html)             |
| Fix USB Keyboard Wake   | SSDT-USBW.aml      | [dortania/usb/keyboard](https://dortania.github.io/OpenCore-Post-Install/usb/misc/keyboard.html#method-2-create-a-fake-acpi-device) |

---

#### Kexts

| Type            | Kext                                                         | Version          | Author                                                                                                                              |
| --------------- | ------------------------------------------------------------ | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Audio           | AppleALC /<br> VodooHDA.kext*                                | 1.9.1 <br> 2.9.9 | [acidanthera/AppleALC](https://github.com/acidanthera/AppleALC) <br> [sourceforge.net](https://sourceforge.net/projects/voodoohda/) |
| Card Reader     | GenericCardReaderFriend.kext                                 | 1.0.4            | [0xFireWolf/GenericCardReaderFriend](https://github.com/0xFireWolf/GenericCardReaderFriend)                                         |
| CMOS Memory     | RTCMemoryFixup.kext                                          | 1.0.7            | [acidanthera/RTCMemoryFixup](https://github.com/acidanthera/RTCMemoryFixup)                                                         |
| CPU Temp        | XHCI-unsupported.kext                                        | 0.9.2            | [RehabMan/OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All/tree/master/XHCI-unsupported.kext)                   |
| Ethernet        | LucyRTL8125Ethernet.kext                                     | 1.1.0            | [Mieze/LucyRTL8125Ethernet](https://github.com/Mieze/LucyRTL8125Ethernet)                                                           |
| Graphics        | WhateverGreen.kext                                           | 1.6.7            | [acidanthera/WhateverGreen](https://github.com/acidanthera/WhateverGreen)                                                           |
| NVMe SSD        | NVMeFix.kext                                                 | 1.1.1            | [acidanthera/NVMeFix](https://github.com/acidanthera/NVMeFix)                                                                       |
| Patch Engine    | Lilu.kext                                                    | 1.6.8            | [acidanthera/Lilu](https://github.com/acidanthera/Lilu)                                                                             |
| Sensors         | VirtualSMC.kext <br> SMCSuperIO.kext <br>  SMCProcessor.kext | 1.3.3            | [acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC)                                                                 |
| USB Map         | USBMap.kext                                                  | 1.0              | [rafaelmaeuer/Z590-P/USB](https://github.com/rafaelmaeuer/Asus-Z590-P-Hackintosh/tree/master/USB/Results/USBMap.kext)               |
| (USB Map Helper | USBInjectAll.kext                                            | 0.7.6            | [Sniki/OS-X-USB-Inject-All](https://github.com/Sniki/OS-X-USB-Inject-All))                                                          |
| USB Wake        | USBWakeFixup.kext                                            | 1.0              | [osy/USBWakeFixup](https://github.com/osy/USBWakeFixup)                                                                             |

*\*Kext needs special setup, see [Docs/AUDIO](Docs/AUDIO.md)*

---

#### Tools

| Name                   | Version   | Download                                                                                                    |
| ---------------------- | --------- | ----------------------------------------------------------------------------------------------------------- |
| Hackintool             | 4.0.3     | [headkaze/Hackintool](https://github.com/headkaze/Hackintool/)                                              |
| ~~Intel Power Gadget~~ | 3.7.0*  🚨 | [software.intel.com](https://software.intel.com/content/www/us/en/develop/articles/intel-power-gadget.html) |
| IORegistryExplorer     | 2.1       | [vulgo/IORegistryExplorer](https://github.com/vulgo/IORegistryExplorer)                                     |
| MaciASL                | 1.6.2     | [acidanthera/MaciASL](https://github.com/acidanthera/MaciASL/)                                              |
| OpenCore Configurator  | 2.75.0.0  | [mackie100projects](https://mackie100projects.altervista.org/download-opencore-configurator/)               |
| USBMap                 | -         | [corpnewt/USBMap](https://github.com/corpnewt/USBMap)                                                       |

*\*This version causes kernel panic after sleep on iMacPro1,1 SMBIOS*

---

#### Troubleshooting

For a list of tips and tricks for already known problems see [Docs/TROUBLE](Docs/TROUBLE.md).

---

### Credits and Documentation

This Hackintosh was build with help of the following repositories and guides:

| Help on Issue                    | Source                                                                                                                        |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Motivation and Hardware          | [SchmockLord/Gigabyte-Z590i-Vision-D-11900k](https://github.com/SchmockLord/Gigabyte-Z590i-Vision-D-11900k)                   |
| BIOS and OpenCore Config         | [yilmazca/intel-i9-10900K-Asus-prime-Z490A](https://github.com/yilmazca/intel-i9-10900K-Asus-prime-Z490A-hackintosh)          |
| F1 Boot Error and BIOS           | [jergoo/Hackintosh-ROG-STRIX-Z490I](https://github.com/jergoo/Hackintosh-ROG-STRIX-Z490I#f1-boot-error)                       |
| OpenCore Config and Installation | [OpenCore Install Guide - Desktop Comet Lake](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html) |
| Installing VoodooHDA             | [yahgoo/installVoodooHDA4BSnMont](https://github.com/yahgoo/installVoodooHDA4BSnMont)                                         |
| Layout for AppleALC              | Mikaël G.                                                                                                                     |

Find more links and documentation in [Docs/LINKS](Docs/LINKS.md).

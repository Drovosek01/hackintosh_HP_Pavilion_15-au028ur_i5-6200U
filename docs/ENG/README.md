# What did I do when installing Hackintosh on a laptop

ENGLISH | [РУССКИЙ](/README.md)

I wrote this instruction for myself, so that after reinstallation I don’t remember what to do. Instructions written after installing macOS Mojave 10.14.6. on a laptop [HP Pavilion 15-au028ur](https://www.support.hp.com/document/c05193511).

## HP Pavilion 15-au028ur Notebook Specifications

* CPU
  * Intel Core i5-6200U 2.3GHz, Turboboost 2.8GHz, Skylake
* Video card
  * Intel HD Graphics 520
  * Nvidia Geforce 940MX
* RAM
  * DDR4 2133MHz
* Motherboard
  * HP 820C v82.39
* BIOS
  * HP Insyde F.52
* Sound adapter
  * Realtek ALC 295
* Bluetooth
  * Realtek Bluetooth 4.0 Adapter
* Wifi
  * Realtek RTL8723BE 802.11 bgn Wi-Fi Adapter
* Ethernet
  * Realtek RTL8139/810x Fast Ethernet Adapter
* Card Reader
  * Realtek PCI-E Card Reader

## What happened and did not work "revive"

### What works

* Intel HD Graphics 520 graphics
* Graphic acceleration Intel Quick Sync
* TurboBoost
* SpeedStep
* Adjust the brightness of the keys Fn + F2 / Fn + F3, as the decrease and increase the brightness, respectively
  (as well as in Windows 10, I specifically made their activation only with Fn)
* Adjust the sound with the Fn + F6 / Fn + F7 / Fn + F8 keys, as "Silent", decrease the volume and increase the volume, respectively
* Adjust the audio playback with the Fn + F10 / Fn + F11 / Fn + F12 keys, like turning on the previous track, playing or pause, turning on the next track
* Keyboard backlight adjustment works using Fn + F5, but the brightness of the keyboard backlight is not adjustable and, most likely, its use is not related to other F keys
* Touchpad as Apple Magic Trackpad - almost all gestures work
* USB 3.0 and USB 2.0 ports
* Sleep
* Port 3.5 mini Jack for headphones
* Built-in speakers
* Stereo microphones
* Webcam
* Ethernet
* Numpad
* Display of battery charge (not always working correctly, often you have to reset CMOS in a laptop, holding the power button for ~ 20 seconds)

### What does not work

* Wifi
* Bluetooth
* Nvidia Geforce 940MX (disabled in macOS using the boot argument `-wegnoegpu`)
* FaceTime, iMassage, HandOff, Continuity - in order to make these functions work, you need Wifi to work (and probably bluetooth, but this is not certain), and you need to buy compatible Wifi (and Bluetooth) on my laptop with macOS Mojave Wifi modules and replace them in a laptop, but I did not want to do this

### What is not checked

* Card Reader
* HDMI
* Drive (it is recognized in macOS and you can even open it by pressing a couple of buttons in the interface, but I do not have DVD/CD disks to check the operation of the drive)

## Pre-installation preparation

Just in case, save all important files to a separate USB flash drive or to the cloud.

Make a report of the system in AIDA64 and archive the EFI folder that you have on the flash drive, and upload it to the cloud so that in case of an unforeseen situation you can correctly describe the situation by attaching files with a description and so that you can be helped.

MacOSX can be installed on a disk (without formatting) only with GPT (GUID Partition Table) markup.

It is recommended to erase (format) the entire disk during MacOSX installation, but this is not necessary.

If you have only 1 disk (1 HDD or 1 SSD) on which Windows is already installed and you want to install MacOSX next to Windows, then there are several solutions:

* During MacOSX installation, erase (format) the entire disk, but then all files will be deleted
* Buy a separate disk and install MacOSX on it
* If your disk is marked up in GPT, then you can separate the partition in Windows and then install MacOSX on it
    * You can find out how marked up is in Windows, to do this, open "Disk Management" (right-click on start), then open the properties of the disk (right-click on the disk itself, and not on sections where it says "Disk 0" or "Disk 1" ), open the "Tom" tab and look at the section style there. If the section style "Table with GUID sections", then everything is fine
    * You can separate or create a partition in Windows in the same Disk Management program. To do this, right-click on the partition from which you will separate another partition and in the context menu, click Compress and then select how many megabytes to compress the selected partition. Accordingly, everything that is larger than these megabytes will be formed into a new unallocated domain, which you can partition into any file system, but better in FAT32. Then, during MacOSX installation, you need to select this partition in Disk Utility, format it in APFA or HFS + (it depends on the version of MacOSX you are installing) and select MacOSX when installing MacOSX
* If your disk is marked in MBR, then you will need to convert it to GPT, or erase (format) in Disk Utility during MacOSX installation
    * You can find out how marked up is in Windows, to do this, open "Disk Management" (right-click on start), then open the properties of the disk (right-click on the disk itself, and not on sections where it says "Disk 0" or "Disk 1" ), open the "Tom" tab and look at the section style there. If the style of the "MBR" section, then it's bad
    * To convert MBR to GPT in Windows without losing data, you need to use third-party programs. As far as I know, these programs "Paragon Hard Disk Manager", "AOMEI Partition Assistant" and "MiniTool Partition Wizard" and, perhaps, any other utilities allow you to convert markup from MBR to GPT without data loss. Unfortunately, only the paid versions of these programs allow you to convert. Personally, I used the "MiniTool Partition Wizard" and everything was converted without data loss. After switching off, you need to switch the boot mode from CSM (Legacy) to UEFI in the BIOS/UEFI settings.

## BIOS/UEFI setting

These parameters are very important.

* Reset to factory settings
* Enable UEFI mode
* Enable AHCI
* Disable Secure Boot
* Set VideoRAM to 64 MB


## Creating a bootable flash drive

1. [Download BootDiskUtility](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)
2. Download [special image](https://applelife.ru/threads/bdu-macos-i-clover-iz-windows-izgotovlenie-zagruzochnoj-flehshki.37189/page-57#post-557498) macOS Mojave 10.14.6 for BDU (this is a file with the .hfs extension, maybe it will be in the archive)
3. Insert the flash drive size of 8 GB or more (in any port)
4. In BDU

   * Open Options -> Configuration
   * Click "Check Now" and wait until the row is updated next
   * Everything else is left to default
   * Click "OK"
   * Select the USB flash drive and press the "Format" button and confirm the action
   
   > When a flash drive is formatted, 2 partitions will be created on it: ESP and an empty partition. On ESP there will already be a Clover loader unpacked from an ISO image from the repository on Sourceforge
   
   * Select the second section (you may need to click on the "+" to the left of the flash drive), it is usually located at the very bottom
   * Press the "Restore" button and select the 5.hfs files
   * We are waiting for the progress bar of the image recording in BDU to end
   * Done

There is also a guide with pictures in a pdf file. This mini manual is called "BDU_FAQ_STARCOM" and [is attached to this](https://applelife.ru/threads/bdu-macos-i-clover-iz-windows-izgotovlenie-zagruzochnoj-flehshki.37189/page-57#post-557498) post.

## Set up a bootable flash drive

After creating a flash drive with a Clover bootloader and the MacOSX system itself, you need to configure the flash drive, or rather the bootloader, because MacOSX just won't install on a non-Apple computer due to the lack of some differences in hardware between Apple computers and regular PCs or laptops.

### Drivers Used

[Drivers List](/docs/ENG/Configuring/InstalledDrivers.md)

### Setting up the config.plist file

[Instructions for configuring the config](/docs/ENG/Configuring/CustomizingConfig.md)

### Used cakes

[Instructions for using kexts](/docs/ENG/Configuring/InstalledKexts.md)

## Installing hackintosh macOS Mojave 10.14.6

Standard MacOSX installation:

1. If you install MacOSX one disk with Windows and the disk is marked up in GPT, then you need to separate the partition in advance to install MacOSX, but if dick is marked up in the MBR, then you need to convert it to GPT or buy a separate one to install MacOSX. Read more in the section "Pre-installation preparation"
2. If you do not need the disk files that are on the disk on which you will install MacOSX, then follow on
3. After setting up the boot drive, insert it into the computer, reboot and go to the BIOS/UEFI or a separate submenu. You need to choose to boot from your flash drive and at the same time when choosing a flash drive in the line with its full name, most likely, there should be the word "UEFI"
4. Boot from the flash drive and get into the Clover loader GUI menu. After that, immediately press any arrows on the keyboard to reset the timer (this timer can be disabled in the config.plist)
5. Switch by arrows, select "Boot macOS Install from ..." and press Enter
6. Wait until the window with the choice of language is loaded and choose the language
7. In the top panel (you need to bring the cursor to the top of the screen) or in the appeared window open the Disk Utility
8. Click on the "View" button in the upper left corner of the window (or in the top panel) and switch the view to "Show all devices"
9. Choose your disk and click the "Erase" button. After installing MacOSX, you can also partition the disk into sections using Disk Utility.
   * Name: you can set any, but probably better in English letters
   * Format: choose APFS
   * Schema: GUID section schema
10. Close the disk utility and select "Install macOS"
11. Select the partition you created in Disk Utility. It will be installed on it. Click to install
12. The process may not last as many minutes as indicated on the screen. Every few minutes, move the cursor so that the computer does not go to sleep
13. When the computer starts to reboot, you need to start booting from your bootable flash drive and in the Clover GUI menu, select "Boot macOS from ..." and press Enter (instead of three dots there will be a section name that you wrote in Disk Utility)
14. Next, perform the manipulation of the initial setup of your hackintosh computer and configure your macOS account. It is advisable to enter everything in English. You can switch the layout (language) using the key combination Ctrl + Space, or Alt + Space, or Win + Space, or use the mouse to change in the upper right corner of the window. All further settings can be changed at any time in the System Settings, so do not be afraid to make a mistake

## Setting up macOS

Below are the most important, in my opinion, points that need to be included on most hackintoshs after installation of the system.

1. In the terminal, enter `sudo spctl --master-disable` to disable Gatekeeper and install applications not only from MacAppstore
2. Enable TRIM for SSD drives using the command in the terminal `sudo trimforce enable`
3. Transfer the file `MyKeyboardBundle.bundle` to`/Library/Keyboard Layouts` and to `/System/Library/Keyboard Layouts` or make this file using the Ukelele program and [guide](https://www.youtube.com/watch?v=Ll6UGWGSSv8). Then go to "System Settings", "Keyboard", "Input Sources" and add a new layout and delete the Russian layout.
4. [Install Clover](https://sourceforge.net/projects/cloverefiboot/) and configure it before installation (the “Configure” button will be on the left of one of the steps)
   - Be sure to tick the first two paragraphs - "Install only for UEFI" and "Install on ESP"
   - If Clover on your flash drive is configured, then the remaining checkboxes can be left unchanged, and if Clover on the flash drive is not configured, then you can configure it in this menu
   - Mount the EFI partition of your disk and flash drive if they are not mounted
   - All files and folders from EFI flash drives are copied to the EFI disk with replacement and reboot

The full list of settings that I use is described in the corresponding file [**MacOSX Setup**](/docs/ENG/Configuring/ConfiguringMacOSX.md)

## Configure Hackintosh

### Sleep Setup

After installing hackintosh, my dream worked incorrectly. If I closed the lid of the laptop or forcibly included sleep by clicking on an apple in the corner, the laptop immediately went to sleep and after a few seconds it turned on.

I was helped to fix this by executing this command in the terminal and, of course, rebooting after the execution:

`sudo pmset -a hibernatemode 0`

And adding the argument `darkwake = 0` to the system boot arguments. Honestly, I didn’t check how a dream will behave on a laptop without this argument.

You can read more about this setup of sleep or hibernation on these links:

* https://bulkin.me/notes/2233
* http://osxh.ru/terminal/command/pmset
* https://www.insanelymac.com/forum/topic/299721-sleep-hibernation-how-it-works-and-how-to-use/

``` xml
<key>boot</key>
<dict>
  <key>HibernationFixup</key>
  <true/>
</dict>
```

Also [vit9696 recommends](https://www.insanelymac.com/forum/topic/304530-clover-change-explanations/?do=findComment&comment=2617018) always enable the `RtcHibernateAware` flag, but everything works fine for me with item off. There are also different parameters in the config that allow you to adjust the hibernation/sleep, you can find out about them in the free book-textbook Clover khaki.

### Installing Windows

[Description of the nuances of installing Windows next to Hackintosh](/docs/ENG/AboutWindows/InstallWindows.md)

### Windows Setup

As a setup for Windows 10 to work with macOS, I needed to set up time synchronization and, for convenience, make a partition for files with the ExFat file system. About ExFat section under the files I wrote above in the instructions for installing Windows.

You can read about time synchronization and find direct manuals there:

* https://appstudio.org/faq/3068.html
* https://www.tonymacx86.com/threads/fix-incorrect-time-in-windows-osx-dual-boot.133719/

## DSDT setting

Using patches for the DSDT file, I managed to get the battery charge indicator displayed and enable screen brightness adjustment with the Fn + F2 and Fn + F3 keys.

[DSDT configuration](/docs/ENG/Configuring/PatchingDSDT.md)

## Installing Software

### Emergency Programs

If you have a hackintosh, and not a real Apple computer, then I recommend that these programs always be installed on your system. These programs are part of the Hackintosh Tools list, but they are most needed.

1. Clover Bootloader https://sourceforge.net/projects/cloverefiboot/
2. CloverConfigurator https://mackie100projects.altervista.org/download-clover-configurator/
3. Plist Edit Pro https://www.fatcatsoftware.com/plisteditpro/

### Hackintosh programs

These programs are used mainly for configuring Hackintosh, as a working macOS tool, they are hardly useful to you. It is advisable to leave some of these programs in your hackintosh in case something goes wrong and the system starts to show off, because not everyone can determine how correctly and how fully your hackintosh is configured.

[Hackintosh tools](/docs/ENG/ProgramsList/HackintoshTools.md)

### Framework software for other programs

These programs are needed for other programs or scripts. This is mainly used by different developers. If you need them, even without this list you will know which program you need.

[Other Software](/docs/ENG/ProgramsList/OtherSoftware.md)

### Installable Software

Most of the programs from this list I use in my daily work. Naturally, the list is not the most complete, see and decide according to your needs.

[Regular Software](/docs/ENG/ProgramsList/RegularSoftware.md)

## Benchmark testing

The list of tests, their description and results are presented in a separate file.

[Benchmark test results](/docs/ENG/BenchmarksTesting/benchmark_testing.md)

## Else

### Wallpapers

You can find wonderful wallpapers on the website https://unsplash.com/

### Forum Topics

In these topics, I published information about configuring and installing hackintosh for this laptop

* https://applelife.ru/threads/hp-pavilion-15-au028ur-skylake-i5-6200u.2944282/
* https://www.tonymacx86.com/threads/guide-hp-pavilion-15-au028ur-skylake-i5-6200u.281106/
* https://www.insanelymac.com/forum/topic/339650-guide-hp-pavilion-15-au028ur-skylake-i5-6200u-10145/
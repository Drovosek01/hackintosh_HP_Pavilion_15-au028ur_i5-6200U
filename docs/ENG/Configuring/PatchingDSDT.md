## Configure DSDT

By applying patches to the DSDT file, I was able to make the battery indicator appear and enable screen brightness adjustment using the Fn+F2 and Fn+F3 keys.

First you need to extract .aml files, disassemble them and fix compilation errors

1. Go to the clover bootloader GUI menu and press F4 or Fn+F4 to save the original ACPI tables of your computer
2. Boot into OSX, mount the ESP and go to `/EFI/CLOVER/ACPI/original` and make sure there is a file with the extension .aml and copy the origianl folder somewhere
3. Download [MaciASL](/docs/ProgramsList/HackintoshTools.md)
4. Create a new folder and copy the DSDT file to it.aml
5. Acting instructions on [osxpc](https://osxpc.ru/faq/acpi-manual/) or [tonymacx86](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/) convert the DSDT file.aml to DSDT file.dsl
6. Open the DSDT file.dsl using MaciASL and click "Compile" at the top of the program window
7. You will see a small window at the bottom of which is written the number of errors and warnings. If there are 0 errors, this is great. If there are errors, look for her wording and Google. You can ignore the warnings

------

I did not work brightness adjustment using the keys Fn+F2 and Fn+F3 (Yes, I BIOS/UEFI included the Fn key to function keys included only with Fn, and normal keys F1-F12 worked without Fn), although the System settings in the "Monitor" brightness was adjusted, but each time to go there would be stupid.

I learned that to adjust the brightness with the F keys, you can use kext ApplePS2SmartTouchpad, either with patches to DSDT. I tried the appleps2smarttouchpad kext, but I didn't like it because it gave me few gestures compared to the VoodooPS2Trackpad. I decided to patch the DSDT to be able to adjust the brightness with F keys. With [this guide](https://www.tonymacx86.com/threads/guide-patching-dsdt-ssdt-for-laptop-backlight-control.152659/)I found out that pressing Fn+F2/F3 DSDT methods _Q10 and _Q11. I found the lines to replace the insides of these methods and made my patch:

```c
into method label _Q10 replace_content
begin
// Brightness Down\n
Notify(\_SB.PCI0.LPCB.PS2M, 0x0205)\n
Notify(\_SB.PCI0.LPCB.PS2M, 0x0285)\n
end;
into method label _Q11 replace_content
begin
// Brightness Up\n
Notify(\_SB.PCI0.LPCB.PS2M, 0x0206)\n
Notify(\_SB.PCI0.LPCB.PS2M, 0x0286)\n
end;
```

To apply it, you need to open the DSDT file.dsl using MaciASL, at the top click "Patch" and in the field where you can type, you need to insert the patch, and then click apply. Most likely, you will be responsible for adjusting the brightness of other methods, and not _Q10 and _Q11, so follow the guide from Rehabman to find out the names of the methods.

Also [patches from olderst](https://github.com/olderst/Keyboard-Patches) for the brightness keys were also similarly able to enable brightness adjustment using Fn+F2/F3

------

Also, I did not display the battery indicator at the top right. I learned that this can only be fixed with a DSDT patch and the use of additional kexts.

For the beginning try to use only kekst for the battery without the use of patches for DSDT. There are several kexts that allow you to display the battery indicator. It is unlikely that they will work without the use of patches, but it's worth a try.

Kexts to display battery:

- [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver/downloads/)
- [VoodooBatterySMC + FakeSMC](https://sourceforge.net/projects/hwsensors3.hwsensors.p/)
- [SMCBatteryManager + VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)

Just do not forget to read the instructions and/or README files with these cupcakes to know the nuances of their installation and configuration. Fakesmc and VirtualSMC are not compatible and only 1 of them should be used. When using kext VirtualSMC also need to uninstall the driver SMCHelper.move the VirtualSMC driver to efi and replace it.efi. Acpibatterymanager and VoodooBatterySMC and SMCBatteryManager are probably not compatible with each other either. All the kexts should be placed in the `/EFI/CLOVER/kexts/Other` folder and preferably after that the kernel cache should be reset by running KextUtility.

If simply using any of these kexts did not help, then you need to patch the DSDT file for the battery indicator to work. Can be done its the patch on instructions on forum [tonymacx86](https://www.tonymacx86.com/threads/guide-how-to-patch-dsdt-for-working-battery-status.116102/) or its shortened version on the forum [olarila](https://olarila.com/forum/viewtopic.php?f=28&t=8208). I tried to make my patch and here's what I got:

```c
#Maintained by: RehabMan for: Laptop Patches
#Battery_HP-Pavilion-15-au028ur.txt

# created by RehabMan 2019-xx-xx
# based on Battery_HP-DV6-1380ek.txt
# additional patches for dv6-1380ek provided by chihab222, credit gsly

# works for:
# HP Pavilion 15-au028ur, per Drovosek

into method label B1B2 remove_entry;
into definitionblock code_regex . insert
begin
Method (B1B2, 2, NotSerialized) { Return (Or (Arg0, ShiftLeft (Arg1, 8)))} \n
end;

# 16-bit EC0 registers
# BADC, 16,
# BFCC, 16,
# MCUR, 16,
# MBRM, 16,
# MBCV, 16,
into device label EC0 code_regex BADC,\s+16, replace_matched begin ADC0,8,ADC1,8, end;
into device label EC0 code_regex BFCC,\s+16, replace_matched begin FCC0,8,FCC1,8, end;
into device label EC0 code_regex MCUR,\s+16, replace_matched begin CUR0,8,CUR1,8, end;
into device label EC0 code_regex MBRM,\s+16, replace_matched begin BRM0,8,BRM1,8, end;
into device label EC0 code_regex MBCV,\s+16, replace_matched begin BCV0,8,BCV1,8, end;

# 16-bit method access
into method label CLRI code_regex (\^.*)MBRM replaceall_matched begin B1B2\(%1BRM0,%1BRM1\) end;
into method label UPBS code_regex (\^.*)MBRM replaceall_matched begin B1B2\(%1BRM0,%1BRM1\) end;
into method label UPBI code_regex (\^.*)BFCC replaceall_matched begin B1B2\(%1FCC0,%1FCC1\) end;
into method label UPBS code_regex (\^.*)MCUR replaceall_matched begin B1B2\(%1CUR0,%1CUR1\) end;
into method label UPBS code_regex (\^.*)MBCV replaceall_matched begin B1B2\(%1BCV0,%1BCV1\) end;
```

But also for me the battery patch for HP Pavilion n012tx worked well. Before applying patches, save a working copy of the DSDT file.dsl in some place. You can find it and apply patches to the battery by opening the DSDT file.dsl in MaciASL by pressing the "Patch" button and in the left sidebar scrolling down to the lines that start with "[bat]". Then try to apply patches for about your laptops. Read the Beginning of each patch, because there at the top of the comments contains useful background information.

I have a battery indicator displayed and the percentages change when charging and discharging, but it often happens that they do not change and have to reset the CMOS by pressing the power button for 15-20 seconds.

---

ACPI code can use the _OSI method (implemented by the ACPI host) to check which Windows version it is running on. Most DSDT implementations will vary the USB configuration depending on the version of Windows that is running.

When running OS X, none of the checks DSDT might be doing for _OSI(“Windows \<version\>”) will return true because it only responds to “Darwin”. This is the reason for the “OS Check Fix” family of DSDT patches. By patching DSDT to simulate a certain version of Windows when running Darwin, we can obtain behavior that would normally happen when running that specific version of Windows.

Rehabman has already made an ACPI file with different variants of checks, but I added it a bit, because now there is already Windows 10 1903. I don't know what version it is, so I wrote "Windows 2019"in SSDT. For this SSDT file to work correctly, you need to rename all the "_OSI" methods to "XOSI" and the easiest way to do this is to make the corresponding patch in the config file.

Here is a link to the file from Rehabman: https://github.com/RehabMan/OS-X-Clover-Laptop-Config/blob/master/hotpatch/SSDT-XOSI.dsl

```xml
<dict>
  <key>Comment</key>
  <string>change _OSI to XOSI</string>
  <key>Disabled</key>
  <false/>
  <key>Find</key>
  <data>
  	X09TSQ==
  </data>
  <key>Replace</key>
  <data>
  	WE9TSQ==
  </data>
</dict>
```

Also, just in case I edited DSDT in that block of code, where there is a check of the conditions on what is the version of Windows and the first line, before the comparisons, I put what is returned, if it is "Windows 2015".

Any visible changes after manipulations with "_OSI" I didn't notice.

---

As far as I know, to work correctly USB ports, especially USB 3.0, you need to remove the extra USB from the "device tree". This can be done manually using instructions from Rehabman: https://www.tonymacx86.com/threads/guide-creating-a-custom-ssdt-for-usbinjectall-kext.211311/ (also, if you Google, you can find more understandable interpretation or translation of this manual).

There is another way, more simply - to generate the necessary files using the [Hackintool]((/docs/ENG/ProgramsList/HackintoshTools.md).) program.

![Hackintool USB tab](https://github.com/Drovosek01/hackintosh_HP_Pavilion_15-au028ur_i5-6200U/blob/master/images/other_images/Hackintool_USB.png?raw=true)

Open Hackintool, tab "USB". Takes a flash drive that supports USB 3.0 and alternately connect to all USB ports and spot what lines in the program are highlighted in green. Then takes the USB stick, which supports only USB 2.0 and also alternately connect to all USB ports.

Then all the ports that neither the times were not cut green isolated and removed. (Alternately select and click on the button with the icon of the circle with a minus). Then click the Export button (it is also at the bottom of the window). Then, in the course of the dialog boxes that appear, you agree with them and choose your config file, some patches will be added to it (you can not choose a config file, but specify any folder, then create a config file exclusively with some patches and you can manually copy them). The desktop will appear .aml files and kext USBPorts. These files are placed in `/CLOVER/ACPI/patched` and `/CLOVER/kexts/Other`, respectively. Add the text USBInjectAll (although I do not know exactly whether it is necessary for these "patches") and reboot.

After doing the manipulation and a few days of using Hackintosh with these cupcakes and SSDT files for USB, I did not notice any visible difference in how the Hackintosh worked before they were applied, but I did not delete them.

---

After applying all patches in the DSDT file.dsl you need to open the "File" tab in MaciASL, choose "Save as", name the file simply DSDT and file format choose "ACPI Machine Language Binary". Then the saved DSDT file.aml needs to move to `/EFI/CLOVER/ACPI/patched` and reboot your Hackintosh.
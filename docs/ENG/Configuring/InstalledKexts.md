### Used kexts

Kexts (kernel extensions) is a Windows driver. In this list, all the kexts are important and they all lie in `/CLOVER/kexts/Other`, but the kext for the touchpad and keyboard (VoodooPS2Trackpad), I had to first install using KextUtility, then remove from /S/L/E and put in `/CLOVER/kexts/Other`, otherwise the touchpad was not recognized and gestures did not work.

Naturally for each configuration of the computer you need a set of kexts and not only the texts affect the performance of the system, but also a variety of patches in the config, DSDT, etc.

* FakeSMC https://sourceforge.net/projects/hwsensors3.hwsensors.p/
* Lilu https://github.com/acidanthera/Lilu
* WhateverGreen https://github.com/acidanthera/WhateverGreen
* VoodooPS2Trackpad https://github.com/acidanthera/VoodooPS2
* AppleALC https://github.com/acidanthera/AppleALC
* RealtekRTL8100 https://www.insanelymac.com/forum/files/file/259-realtekrtl8100-binary/ | https://github.com/Mieze/RealtekRTL8100
* ACPIMonitor https://sourceforge.net/projects/hwsensors3.hwsensors.p/
* VoodooBatterySMC https://sourceforge.net/projects/hwsensors3.hwsensors.p/
* ACPIKeyboard https://bitbucket.org/RehabMan/os-x-acpi-keyboard/downloads/
* USBInjectAll https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/
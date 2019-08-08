### Используемые кексты

Кексты (kernel extensions) это как в Windows драйвера. В этом списке все кексты важны и все они лежат в `/CLOVER/kexts/Other`, но кекст для работы тачпада и клавиатуры (VoodooPS2Trackpad), мне пришлось сначала установить с помощью программы KextUtility, потом удалить из /S/L/E и поместить в `/CLOVER/kexts/Other`, иначе тачпад не распознавался и не работали жесты.

Естественно для каждой конфигурации компьютера нужен свой набор кекстов и не только кексты влияют на работоспособность системы, но еще и разнообразные патчи в конфиге, DSDT и т.д.

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
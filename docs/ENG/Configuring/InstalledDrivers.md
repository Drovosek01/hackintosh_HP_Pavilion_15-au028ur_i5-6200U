### Driver to be used

Drivers must be in the `/CLOVER/drivers/UEFI` folder if you have Clover revision 4978 and above or `/CLOVER/drivers64UEFI` if you have Clover revision 4972 and below. Some drivers are required (for example, SMS Helper or FSInject and others), and some can be dispensed with (for example, drivers to control the mouse cursor in the bootloader GUI). The description of most of the drivers you can find in the book "[Clover of Hacky Color](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", or [here](https://vk.com/topic-12954845_40124589). Also with some of the text can be provided with their own drivers that can be used instead of existing or complement them.

#### These are the drivers I use in my Mac laptop

Important drivers

- ApfsDriverLoader
- AptioMemoryFix

  > Since the Clover 4978 revision, the AptioMemoryFix driver is not included in the Clover loader, but you can download it yourself from the official repository: https://github.com/acidanthera/AptioFixPkg or use one of the OsxAptioFix3Drv.efi, OsxAptioFix2Drv.efi, OsxAptioFixDrv.efi and last but not least OsxLowMemFix.efi, but I still recommend using only AptioMemoryFix

- FSInject
- SMCHelper
- VBoxHfs

Not important drivers, but their installation does not hurt (at least not hurt in my case)

- AudioDxe
- DataHubDxe
- Fat
- Ps2MouseDxe
- UsbKbDxe
- UsbMouseDxe
- VBoxExt2
- VBoxExt4
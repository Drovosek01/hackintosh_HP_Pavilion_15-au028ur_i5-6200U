### Используемые драйвера

Драйвера должны быть в папке `/CLOVER/drivers/UEFI`, если у вас Clover ревизии 4978 и выше или `/CLOVER/drivers64UEFI`, если у вас Clover ревизии 4972 и ниже. Некоторые драйвера обязательны для использования (например SMCHelper или FSInject и другие), а без некоторых можно обойтись (например драйвера для управления курсором мыши в GUI загрузчика). Описание большей части драйверов вы можете найти в книги "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", или [здесь](https://vk.com/topic-12954845_40124589). Так же с некоторыми кекстами могут предоставляться собственные драйвера, которые могут использоваться вместо существующих или дополнять их.

#### Эти драйвера я использую в своем макинтош ноутбуке

Важные драйвера

- ApfsDriverLoader
- AptioMemoryFix

  > Начиная с ревизии Clover 4978 драйвер AptioMemoryFix не входит в состав загрузчика Clover, но его можно скачать самостоятельно с официального репозитория: https://github.com/acidanthera/AptioFixPkg или использовать один из OsxAptioFix3Drv.efi, OsxAptioFix2Drv.efi, OsxAptioFixDrv.efi и в последнюю очередь OsxLowMemFix.efi, но я все же рекомендую использовать исключительно AptioMemoryFix

- FSInject
- SMCHelper
- VBoxHfs

Не важные драйвера, но их установка никак не навредит (по крайней мере не навредила в моем случае)

- AudioDxe
- DataHubDxe
- Fat
- Ps2MouseDxe
- UsbKbDxe
- UsbMouseDxe
- VBoxExt2
- VBoxExt4
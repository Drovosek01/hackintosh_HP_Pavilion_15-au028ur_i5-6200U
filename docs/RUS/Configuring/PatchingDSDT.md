## Настройка DSDT

С помощью применения патчей для файла DSDT, мне удалось заставить отображаться индикатор заряда батареи и включить регулировку яркости экрана с помощью клавиш Fn+F2 и Fn+F3.

Сначала нужно извлечь .aml файлы, дизасемблировать их и исправить ошибки компиляции

1. Перейдите в GUI меню загрузчика Clover и нажмите F4 или Fn+F4, чтобы сохранились оригинальные ACPI таблицы вашего компьютера
2. Загрузитесь в MacOSX, примонтируйте ESP и перейдите в `/EFI/CLOVER/ACPI/original` и убедитесь, что там есть файлы с расширением .aml и скопируйте папку origianl куда-нибудь
3. Скачайте [MaciASL](/docs/ProgramsList/HackintoshTools.md)
4. Создайте новую папку и скопируйте в нее файл DSDT.aml
5. Действуя инструкции на [osxpc](https://osxpc.ru/faq/acpi-manual/) или на [tonymacx86](https://www.tonymacx86.com/threads/guide-patching-laptop-dsdt-ssdts.152573/) преобразуйте файл DSDT.aml в файл DSDT.dsl
6. Откройте файл DSDT.dsl с помощью MaciASL и нажмите кнопку "Скомпилировать" в верху окна программы
7. У вас появится маленькое окно внизу которого написано количество ошибок и предупреждений. Если ошибок 0, это замечательно. Если ошибки есть, найдите ее формулировку и гуглите. На предупреждения можно не обращать внимание

------

У меня не работала регулировка яркости с помощью клавиш Fn+F2 и Fn+F3 (да, я в BIOS/UEFI включил клавишу Fn, чтобы функциональные клавиши включались только вместе с Fn, а обычные клавиши F1-F12 работали без Fn), хотя в Системных настройках в пункте "Монитор" яркость регулировалось, но каждый раз заходить туда было бы глупо.

Я узнал, что настроить регулировку яркости с помощью F клавиш можно с помощью кекста ApplePS2SmartTouchpad, либо с помощью патчей в DSDT. Я попробовал кекст ApplePS2SmartTouchpad, но мне он не понравился, т.к. по сравнению с VoodooPS2Trackpad он давал мне мало жестов. Я решил пропатчить DSDT, чтобы можно было регулировать яркость F клавишами. С помощью [этого гайда](https://www.tonymacx86.com/threads/guide-patching-dsdt-ssdt-for-laptop-backlight-control.152659/), я узнал, что при нажатии клавиш Fn+F2/F3 в DSDT вызываются методы _Q10 и _Q11. Я нашел строчки на которые нужно заменить внутренности этих методов и сделал свой патч:

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

Чтобы его применить нужно открыть файл DSDT.dsl с помощью MaciASL, вверху нажать кнопку "Патч" и в поле, в котором вы можете набирать текст, нужно вставить этот патч, а потом нажать применить. Скорее всего  за регулировку яркости у вас будут отвечать другие методы, а не _Q10 и _Q11, поэтому следуйте гайду от Rehabman, чтобы выяснить названия методов.

Так же [патчи от olderst](https://github.com/olderst/Keyboard-Patches) для клавиш регулировки яркости тоже аналогичным образом смогли включить регулировку яркости с помощью Fn+F2/F3

------

Так же у меня не отображался индикатор заряда батареи справа вверху. Я узнал, что это можно исправить только с помощью патча DSDT и использования дополнительных кекстов.

Для начала попробуйте использовать только кекст для батареи без применения патчей для DSDT. Есть несколько кекстов, позволяющих отобразить индикатор заряда батареи. Вряд ли они заработают без применения патчей, но стоит попробовать.

Кексты для отображения заряда батареи:

- [ACPIBatteryManager](https://bitbucket.org/RehabMan/os-x-acpi-battery-driver/downloads/)
- [VoodooBatterySMC + FakeSMC](https://sourceforge.net/projects/hwsensors3.hwsensors.p/)
- [SMCBatteryManager + VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)

Так же не забывайте читать инструкцию и/или README файлы с этими кекстами, чтобы знать нюансы их установки и настройки. Кексты FakeSMC и VirtualSMC не совместимы и нужно использовать только 1 из них. При использовании кекста VirtualSMC так же нужно удалить драйвер SMCHelper.efi и на его место переместить драйвер VirtualSMC.efi. Кексты ACPIBatteryManager и VoodooBatterySMC и SMCBatteryManager скорее всего тоже не совместимы между собой. Все кексты нужно помещать в папку `/EFI/CLOVER/kexts/Other` и, желательно, после этого сбрасывать кэш ядра с помощью запуска программы KextUtility.

Если просто использовании какого-либо из этих кекстов не помогло, то нужно пропатчить файл DSDT для работы индикатора заряд батареи. Можно сделать свой патч по инструкции на форуме [tonymacx86](https://www.tonymacx86.com/threads/guide-how-to-patch-dsdt-for-working-battery-status.116102/) или ее сокращенной версии на форуме [olarila](https://olarila.com/forum/viewtopic.php?f=28&t=8208). Я пробовал сделать свой патч и вот, что у меня получилось:

```c
#Maintained by: RehabMan for: Laptop Patches
#Battery_HP-Pavilion-15-au028ur.txt

# created by RehabMan 2019-xx-xx
# based on Battery_HP-DV6-1380ek.txt
# additional patches for dv6-1380ek provided by chihab222, credit gsly

# works for:
#  HP Pavilion 15-au028ur, per Drovosek

into method label B1B2 remove_entry;
into definitionblock code_regex . insert
begin
Method (B1B2, 2, NotSerialized) { Return (Or (Arg0, ShiftLeft (Arg1, 8))) }\n
end;

# 16-bit EC0 registers
#                BADC,   16,
#                BFCC,   16,
#                MCUR,   16,
#                MBRM,   16,
#                MBCV,   16,
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

Но также для меня хорошо сработал патч батареи для HP 3165sf. Перед тем как применять патчи сохраните рабочую копию файла DSDT.dsl в каком-нибудь месте. Вы можете его найти и применить патчи для батареи открыв файл DSDT.dsl в MaciASL, нажав кнопку "Патч" и в левой боковой панели пролистав до строчек, которые начинаются с "[bat]". Дальше пробуй применить патчи для примерно ваших ноутбуков. Читайте Начало каждого патча, потому что там вверху в комментариях содержится полезная справочная информация.

У меня индикатор заряда батареи отображается и проценты изменяются при зарядке и разрядке, но часто бывает, что они не меняются и приходится сбрасывать CMOS с помощью зажатия кнопки питания на 15-20 секунд.

После применения всех патчей в файле DSDT.dsl вам нужно в MaciASL открыть вкладку "Файл", выбрать "Сохранить как", назвать файл просто DSDT и формат файла выбрать "ACPI Machine Language Binary". Потом сохраненный файл DSDT.aml нужно переместить в `/EFI/CLOVER/ACPI/patched` и перезагрузить ваш хакинтош.
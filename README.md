# Что я сделал при установки Hackintosh на ноутбук

Эту инструкцию я писал для себя, чтобы после переустановки не вспоминать что и как делать. Инструкция написана после установки macOS Mojave 10.14.5. на ноутбук HP Pavilion 15-au028ur.

## Характеристики ноутбука HP Pavilion 15-au028ur

* Процессор
  * Intel Core i5-6200U 2.3GHz, Turbobust 2.8GHz, Skylake
* Видеокарта
  * Intel HD Graphics 520
  * Nvidia Geforce 940MX
* ОЗУ
  * DDR4 2133MHz
* Системная плата
  * HP 820C v82.39
* BIOS
  * HP Insyde F.52
* Звуковой адаптер
  * Realtek ALC 295
* Bluetooth
  * Realtek Bluetooth 4.0 Adapter
* Wifi
  * Realtek RTL8723BE 802.11 bgn Wi-Fi Adapter
* Ethernet
  * Realtek RTL8139/810x Fast Ethernet Adapter
* Card Reader
  * Realtek PCI-E Card Reader

## Создание загрузочной флешки

1. Скачиваем BootDiskUtility
2. Скачиваем оригинальный образ macOS Mojave 10.14.5
3. В BDU ????

## Установка macOS Mojave 10.14.5

1. Стандартная установка macOS
2. Разбить диск на разделы сейчас или потом ?????

## Настройка Hackintosh

1. В терминале вводим `sudo spctl --master-disable`, чтобы отключить Gatekeeper и устанавливать приложениея не только из MacAppstore
2. Включить TRIM для SSD дисков с помощью команды в терминале `sudo trimforce enable`
3. Настроить Finder:
    * (Все указанные пункты должны быть отмечены, а не указанные - выключены)
    * В "Основные"
      * Показывать на рабочем столе
        * Жесткие диски
        * Внешние диски
        * CD, DVD и iPod
      * Показывать в новых окнах Finder "<имя_пользователя>"
    * В "Боковое меню"
      * В "Избранное" отметить по усмотрению
      * В "Места" отметить все пункты
      * Включить "Недавние теги"
    * В "Дополнения"
      * Включить "Показывать все расширения имен файлов"
      * Включить "Предупреждать при изменении расширения"
      * Включить "Показывать предупреждение перед удалением из iCloud Drive"
      * Включить "Предупреждать при очистке корзины"
      * Включить "Отображать папки вверху списка"
        * "В окнах при сортировке по имени"
        * "На рабочем столе"
      * Включить "При выполнении поиска Искать на этом Mac"
    * Настроить "Панель инструментов" - открыть любую папку, ПКМ по панели инструментов и выбрать удобные пункты (Создать новую папку, Информация о выделенном, Удалить выделенное)
4. В "Системные настройки"
    * В "Основные"
      * Выбрать оформление "Темное"
      * Выбрать "Спрашивать, сохранять ли изменения при закрытии документа"
      * Выбрать "Веер-браузер по умолчанию" - Google Chrome
      * Возможно отключить сглаживание шрифтов, чтобы убрать жирность у текста
    * В "Рабочий стол и заставка"
      * Выбрать фон для рабочего стола
      * Во вкладке "Заставка" выбрать заставку, время через которое она запускается и отметить пункт "Показывать с часами"
    * В "Dock"
      * Отрегулировать размер Dock
      * Отрегулировать увеличение иконок при наведении курсора на них
    * В "Мониторы" открыть вкладку "Цвета" и выбрать sRGB
    * В "Экономия энергии" настроить режимы при питании от батареи и от розетки
    * Настроить "Мышь"
    * В "Пользователи и группы" открыть "Параметры входа" и установить автоматический вход для пользователя
    * В "Общий доступ" изменить или оставить имя компьютера
    * В "Клавиатура" нажать "Клавиши модификации"и поменять местами Command и Ctrl
    * В "Универсальный доступ"
      * В "Увеличение" включить и настроить увеличение по удобству (до этого решить нужно ли менять местами Ctrl и Command)
      * В "Мышь и трекпад" в "Параметры трекпада"
5. Удалить из Dock лишние программы
6. Перекинуть файл `MyKeyboardBundle.bundle` в `/Library/Keyboard Layouts` и в `/System/Library/Keyboard Layouts` или сделать этот файл с помощью программы Ukelele и [гайда](https://www.youtube.com/watch?v=Ll6UGWGSSv8). Потом перейти в "Системные настройки", "Клавиатура", "Источники ввода" и добавить новую раскладку и удалить Русскую раскладку.

## Установка программ

### Программы первой необходимости

1. Clover Bootloader
2. CloverConfigurator
3. Plist Edit Pro

### Hackintosh программы

1. KextUtility http://cvad-mac.narod.ru/index/0-4
2. KextBeast 2.0.2 https://www.tonymacx86.com/resources/kextbeast-2-0-2.399/
3. MaciASL by Rehabman https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/
4. MaciASL from github https://github.com/acidanthera/MaciASL
5. Clover Theme Manager https://www.insanelymac.com/forum/topic/302674-clover-theme-manager/
6. IORegistryExplorer 2.1 https://github.com/vulgo/IORegistryExplorer
7. DPCI Manager https://sourceforge.net/projects/dpcimanager/
8. EFI Mounter v3 https://www.tonymacx86.com/resources/efi-mounter-v3.280/
9. Intel Power Gadget https://software.intel.com/en-us/articles/intel-power-gadget
10. ShowHiddenFiles https://gotoes.org/sales/ShowHiddenFilesMacOSX/How_To_Show_Hidden_Files.php
11. Punto Switcher https://yandex.ru/soft/punto/
12. ML Switcher https://apps.apple.com/app/mlswitcher/id422365812
13. Hackintool https://www.tonymacx86.com/threads/release-hackintool-v2-6-6.254559/#post-1764779
14. (Old) Chameleon Wizard https://mac.softpedia.com/get/Utilities/Chameleon-Wizard.shtml
15. (Old) Kext Wizard https://mac.softpedia.com/get/Utilities/Kext-Wizard.shtml

### Программы-фреймворки для работы других программ

1. Java https://www.java.com/
2. Python https://www.python.org/
3. .Net Framework https://dotnet.microsoft.com/download
4. Nodejs https://nodejs.org/
5. Adobe Flash Player - сейчас почти нигде не нужен

### Устанавливаемое ПО

1. Google Chrome <https://www.google.ru/chrome/>
2. Keka <https://www.keka.io/>
3. Sublimetext <http://www.sublimetext.com/>
4. Screenflow
5. VLC Media Player <https://www.videolan.org/vlc/>
6. Git Bash <https://git-scm.com/>
8. Typora <https://typora.io/>
9. Transmission https://transmissionbt.com/
10. Office
11. AppCleaner https://freemacsoft.net/appcleaner/
12. XCode https://developer.apple.com/download/more/
13. Folx
14. Firefox <https://www.mozilla.org/ru/firefox/new/>
15. XnConvert <https://www.xnview.com/en/xnconvert/>
16. XnView <https://www.xnview.com/>
17. Adobe Photoshop
18. HashTab http://implbits.com/products/hashtab/

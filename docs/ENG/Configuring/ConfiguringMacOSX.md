## Configure MacOSX

1. In the terminal, enter `sudo spctl --master-disable` to disable Gatekeeper and install applications not only from MacAppstore
2. Enable TRIM for SSD drives using the command in the `sudo trimforce enable`terminal
3. To Configure Finder:
   - (All items must be marked, not marked - off)
   - mainly"
     - Show on desktop
       - Hard drive
       - External drive
       - CD, DVD and iPod
     - Show in new Finder Windows "<username>"
   - Side menu"
     - In the "favorites" mark at the discretion of the
     - In "Places" mark all items
     - Enable "Recent tags"
   - in addition"
     - Enable "Show all file name extensions"
     - Enable "Warn before changing an extension"
     - Enable "Show warning before deleting from iCloud Drive"
     - Enable the "Warn before emptying the trash"
     - Enable "Show folders at the top of the list"
       - "In Windows when sorted by name"
       - "On the desktop"
     - Include "When a search is performed to find the Mac"
   - Customize the "Toolbar" - open any folder, PKM on the toolbar and select convenient items (Create a new folder, Information about the selected, Delete the selected)
4. in system preferences"
   - mainly"
     - Choose the design "Dark"
     - Select "Ask whether to save changes when closing the document"
     - Choose the "Fan-a" default browser - Google Chrome
     - It is possible to disable font smoothing to remove the fat content of the text
    In the "desktop and screen saver"
     - Choose a background for your desktop
     - In the "Screensaver" tab, select the screensaver, the time after which it starts and mark the "Show with clock" item"
   - in the dock"
     - To adjust the size of the Dock
     - Adjust the magnification of icons when you hover over them
   - In "Monitors" open the "Colors" tab and choose sRGB
   - In the "energy Saving" mode setting when powered from batteries and from the wall outlet
   - Customize "Mouse"
   - In "Users and groups" open "login Options" and set automatic login for user
   - In the "General access" to change or write the name of the computer
   - In "Keyboard" press "modification Keys"and swap Command and Ctrl
   - In "Universal access"
     - In the "Zoom" to enable and configure the increase in convenience (before that, decide whether to swap Ctrl and Command)
     - In "Mouse and trackpad" in "trackpad Options"
5. Remove unnecessary programs from the Dock
6. [Install Clover](https://sourceforge.net/projects/cloverefiboot/) and configure it before installation (on the left of one of the steps will be the "configure" button")
   - Be sure to check the first two items - "Install only for UEFI" and "Install on ESP"
   - If Clover on your flash drive is configured, the remaining checkboxes can not be changed, and if Clover on the flash drive is not configured, then you can configure it in this menu
   - Mount the EFI partition of your disk and flash drive if they are not mounted
   - All files and folders with EFI stick copy to the EFI disk with the replacement and reboot
7. Flip the `MyKeyboardBundle ' file.bundle` in `/Library/Keyboard Layouts` and ' /System/Library/Keyboard Layouts` or make this file using the program Ukelele and [Hyde](https://www.youtube.com/watch?v=Ll6UGWGSSv8). Then go to "System settings", "Keyboard", "input Sources" and add a new layout and remove the Russian layout.
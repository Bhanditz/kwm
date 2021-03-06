# K-Meleon Window Manager
A window management tool for K-Meleon in Microsoft Windows.

## Description
K-Meleon Window Manager is a tiny open-source application (~4MB of RAM) which removes the title bar of K-Meleon, integrates the window buttons into the K-Meleon interface, and adds hotkey and tray controls for K-Meleon.

## Purpose
K-Meleon is a wonderful lightweight fully featured web browser, but one problem is its somewhat clunky outdated reliance on a separate title bar. KWM gives K-Meleon a more minimalistic modern interface similar to Firefox or Chrome by removing the system titlebar and integrating the window buttons into the web browser interface itself.

I originally created this because I was unsatisfied with the currently existing methods of removing the title bar. Using the built in fullscreen settings (or fullscreen2plus) is a workaround that removes the title bar by entering fullscreen mode while leaving the taskbar and toolbars. This is unsatisfactory unless you keep K-Meleon maximized 100% of the time. If you want to have multiple windows on your screen at once, that solution no longer functions, but K-Meleon Window Manager will work under any circumstances.

## Installation
1. Install the latest versions of K-Meleon from http://sourceforge.net/projects/kmeleon/ and AutoHotkey from http://www.autohotkey.com/.
2. Download and extract zip from this page.
3. Run install.bat and check for errors before closing the window.

Optionally, you may remove AutoHotkey after the installation is complete. install.bat will automatically compile and install the application as soon as it is executed (no prompts). Start menu, taskbar, and desktop shortcuts *should* be replaced with one that autostarts KWM with K-Meleon. If you have custom shortcuts and they don't work with KWM, you should copy the k-meleon.lnk file that gets created by install.bat into whatever location you desire (check out the Autostart section of Manual Install for more details about default shortcut locations). If you update K-Meleon and your shortcuts stop working with KWM, you can just run shortcut.bat and they should get fixed.

This git repo contains purely source code (and a few images), so installation and uninstallation are handled with batch scripts. I will eventually create a binary installer and will upload it to my website (not github, I'll put a link here when it's done). The binary installer will allow you to install KWM without needing AutoHotkey.

You can also manually compile and install the application. See below for more details.

## Usage
Start K-Meleon as normal. The shortcut should have been replaced to a shortcut leading to a batch file which will start KWM automatically with K-Meleon. When KWM is running, it will automatically remove the title bar from any K-Meleon window as soon as it becomes active. KWM will automatically terminate when all K-Meleon windows are closed.

#### Window Buttons
During installation, new window buttons ( _ [] X ) are added to K-Meleon as a toolbar. Ensure that the K-Meleon Window Manager toolbar is active, then click and drag it to anywhere you wish (such as the top right of the window). You can right click these buttons for more options. You can also switch them out for OS X style window buttons by modifying your toolbar.cfg file to use the osx bmp variants.

#### Tray Icon
KWM creates a tray icon. Right click to see the available actions and settings.

#### Hotkeys / Keybinds
* W-L (hold the windows key and then left click): Cycles titlebar state. On the first press, it will bring back the title bar on any activated K-Meleon window, on the next press it will return back to the initial state of the program, and so on.
* W-R (hold the windows key and then right click): Opens window management menu with options such as minimize, maximize/restore, close, and the entire tray menu. By default this hotkey now can be used for any application in Windows, but if you uncomment (delete the ; from) lines ?? and ?? of the ahk file before compiling, it will make it so this hotkey only works in K-Meleon.

## Manual Installation
The install.bat file automatically executes all of the steps in this section except step 1. All you have to do is run install.bat. In case there is a problem with the install.bat installation method, you can install it manually: 

1. Download and install AutoHotkey from http://www.autohotkey.com/. You can uninstall AutoHotkey when you are finished compiling.
2. You have the choice of using AutoHotkey's default icon, or using the defaut K-Meleon icon:
  1. If you wish to have the letter H as the program's icon, navigate to and right click core\kwm.ahk and click "compile," and in the same directory as your .ahk file there will be a new file called kwm.exe.
  2. If instead you wish to use my icon (whatever icon you choose will be visible in the tray), follow these steps:
    1. Then open "Convert .ahk to .exe" which should now be in your start menu under AutoHotkey.
    2. For Source, select the ```core\kwm.ahk```
    3. For destination, choose a new name and save location (```kwm.exe```)
    4. For Custom Icon, select ```icons\k-meleon.ico```
    5. Click convert, and now you have compiled an .exe file with the name, location, and icon of your choosing.
3. Run the file (double click) and now it is active, all K-Meleon windows will behave in the new way I have described. Without any further work, you must manually start this application when you want it to work.

#### Autostart
To make it start with K-Meleon (KWM quits when all K-Meleon windows are closed, so you will probably want to follow these steps):

1. Move ```core\kwm.exe``` and ```core\kwm.bat``` to the K-Meleon directory (```C:\Program Files (x86)\K-Meleon``` in 64-bit Windows)
2. Right click the batch file and create a shortcut.
3. Rename your new shortcut to ```K-Meleon.lnk```
4. Right click the shortcut and go to properties
5. Click "Change Icon"
6. Browse and navigate to ```C:\Program Files (x86)\K-Meleon``` and select ```k-meleon.exe```
7. Select the first icon (or whatever you want) and hit OK, then OK again.
8. Copy this new shortcut to both of these locations, replacing the old shortcuts.
  * ```C:\ProgramData\Microsoft\Windows\Start Menu\Programs```
  * ```%appdata%\Microsoft\Windows\Start Menu\Programs```
9. If you have a desktop (or quick launch in XP) shortcut to K-Meleon, replace it with that one also.
10. If you have K-Meleon pinned to your taskbar (Windows 7, 8, 10), navigate to ```%appdata%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar```
11. There should be a file called something like K-Meleon Web Browser. Copy your newly made shortcut into this directory.
12. If it has the same name as the original, let it overwrite. If they have different names, delete the original and rename yours (only the one in TaskBar) to the name that the original had.
13. Now all of your K-Meleon shortcuts open KM TitleBar Delete along with K-Meleon.

#### Window Buttons: _ [] X 
14. Manually copy all of the text in ```core\kwm-toolbar.cfg``` to the bottom of ```C:\Program Files (x86)\K-Meleon\browser\defaults\settings\toolbars.cfg```.
15. Make sure the K-Meleon Window Manager toolbar is enabled in K-Meleon and click and drag it to wherever you would like.

## Known Issues
If you come up with a solution to any of these, please submit a pull request. Collaboration is encouraged!
* In Windows 10, if a shortcut is created on the taskbar leading to kwm.bat, when the application is launched it creates a new taskbar icon. This results in "quick start"-like functionality as seen in early Windows releases and is less than ideal in a modern Windows system. In Windows 7 we get the desired functionality, but for some reason Windows 10 is finicky about batch file shortcuts.
* In Windows 7, the first time you use a pinned taskbar icon, you might run into issues restoring a minimized window. Closing the application and restarting it has always resolved this problem permanently for me. For the first use after installation, you may want to open K-Meleon and immediately minimize it and see if you can restore it. If not, close it and restart the application. The problem should not repeat itself after this.
* Every time the application is updated, three garbage lines are added to toolbar.cfg. These lines do not have any effect on the functionality of K-Meleon, but it is clutter that would ideally be avoided. This occurs because the commenting system employed by K-Meleon config files is buggy. The problem is that you cannot add comments to lines that contain the prime functionality of toolbar buttons without sacrificing the functionality of the button. If this is fixed by K-Meleon developers, then the kwm-toolbar.cfg can be changed to have the #kwm tag added to those lines, in which case they will be replaced rather than supplemented upon update. In the meantime, the user may manually remove these garbage lines if they so desire, but this is not necessary.

As of the publication of this README, I have only tested the latest version of KWM in Windows 7 x64 and Windows 10 x64. In Windows XP x86 I have only tested the original version of KWM which is totally different from the current version. It was only one file at the time with no installer, but the core functionality of the application was similar so it should work in XP as long as the installer works. If you experience any problems, please report bugs using the Issues tab (!) on the right side of the kwm repository.

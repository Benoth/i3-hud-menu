i3-hud-menu
===========

Provides a way to run menubar commands through dmenu.

Dependencies
============
* python-dbus
* dmenu or rofi
* appmenu-qt
* unity-gtk2-module
* unity-gtk3-module

Setup
============
1. sudo apt-get install python3 python-dbus dmenu appmenu-qt unity-gtk2-module unity-gtk3-module
2. i3-appmenu-service.py should be started (with python 3+) on the session's startup.
3. The following should be added to the user's .profile:

    ```
    if [ -n "$GTK_MODULES" ]
    then
      GTK_MODULES="$GTK_MODULES:unity-gtk-module"
    else
      GTK_MODULES="unity-gtk-module"
    fi

    if [ -z "$UBUNTU_MENUPROXY" ]
    then
      UBUNTU_MENUPROXY=1
    fi
   ```

4. i3-hud-menu-{type}.py should be bound to run (with python 3+) with a shortcut (such as a keyboard shortcut).

Usage
============
The user should active the shortcut when the window they wish to show the application menu entries for has focus.  This will open the dmenu at the top.  The user can then use the keyboard to search and navigate the entries.  Pressing enter will execute the selected entry and pressing escape will close the dmenu without executing anything.

Explanation
============
i3-appmenu-service.py  is an implementation of the com.canonical.AppMenu.Registrar DBus service.  Applications exporting their menu through dbusmenu need this service to run.
i3-hud-menu-{type}.py tries to get the menu of the currently focused X11 window, lists possible actions and asks the user which one to run (type is either dmenu or rofi).

Source
============
https://jamcnaughton.com/2015/10/19/hud-for-xubuntu/

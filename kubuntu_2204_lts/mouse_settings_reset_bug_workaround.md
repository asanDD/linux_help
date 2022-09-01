
Mouse settings reset bug workaround
===================================

**Bugreport:**<br>
https://bugs.kde.org/show_bug.cgi?id=435113 <br>
Mouse speed resets to default settings after suspend or replugging the mouse in KDE 5.24.4

**workaround:**<br>
Create a .desktop file with the following content.<br>
`$ nano ~/.local/share/applications/apply_mouse_settings.desktop`

    [Desktop Entry]
    Categories=Utility;
    Comment=A script to reapply the mouse settings
    Exec=sh -c 'kcminit kcminit /usr/lib/qt/plugins/plasma/kcms/systemsettings/kcm_mouse.so'
    GenericName=
    Icon=input-mouse-symbolic
    MimeType=
    Name=Apply mouse settings
    Path=
    StartupNotify=true
    Terminal=false
    TerminalOptions=
    Type=Application
    X-DBUS-ServiceName=
    X-DBUS-StartupType=
    X-KDE-SubstituteUID=false
    X-KDE-Username=

Choose a nice icon for the .desktop file and pin it to the taskbar. Click on that icon to reapply the mouse settings.

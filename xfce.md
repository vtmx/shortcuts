# xfce

## Command to enable gtk debug shortcut
```
gsettings set org.gtk.Settings.Debug enable-inspector-keybinding true
Ctrl + Shift + d
Ctrl + Shift + i

Or 
GTK_DEBUG=interactive your-app

https://gtkthemingguide.surajmandal.in/#/getting_started
```

## Reload theme

```
xfconf-query -c xfwm4 -p /general/theme -s <theme-name>
xfconf-query -c xsettings -p /Net/ThemeName -r && xfconf-query -c xsettings -p /Net/ThemeName -s [theme-name]
```

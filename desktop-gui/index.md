---
title: Desktop GUI
---

# Gnome

Extension management  
 [https://extensions.gnome.org](https://extensions.gnome.org) \# Webpage can request access to Gnome on system  
 Recover off-screen window:  
  `alt-space`, `down arrow`, `enter` \(Select Maximize in off-screen pull-down menu\)

## Create desktop shortcut:

Install GUI application 'Main Menu'

## To Organize

Add to dock:  
Search in application launcher. Right click -> Add to Favorites.

Enter text shell from login GUI:  
  `ctrl-alt-F3`  

 Open terminal  
  `Super-T`

'Legacy' status icons \(application menus, including Dropbox, Jetbrains\)  
[https://pop.system76.com/docs/status-icons/](https://pop.system76.com/docs/status-icons/)  

# Other

Install pinyin roman characters with tone marks
```
	sudo apt install ibus-m17n
	sudo apt install ibus-pinyin
	ibus restart
```

Share Internet connection over Ethernet:
  `nm-connection-editor`

Learn to more easily resize windows: https://askubuntu.com/questions/25670/is-there-any-way-to-make-the-window-resizing-less-sensitive

Gnome
  Force move file (vs copy): drag while holding shift

Recover sound from 'dummy output' (audio / headphones)
[Source](https://www.linuxquestions.org/questions/linux-hardware-18/ubuntu-18-04-dummy-output-and-sound-disappeared-4175659386/)

```
killall pulseaudio
pulseaudio -k
```

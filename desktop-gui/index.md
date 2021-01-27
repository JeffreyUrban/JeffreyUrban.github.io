---
title: Desktop GUI
---

# Gnome

## Extension management  

[Extension Management](https://extensions.gnome.org) 

_Webpage can request access to Gnome on system_

## Recover off-screen window:  

Steps to select Maximize in off-screen pull-down menu:

`alt-space`, `down arrow`, `enter` 

## Create desktop shortcut:

Install GUI application 'Main Menu'

## Add to dock

Search in application launcher. Right click -> Add to Favorites.

## Enter text shell from login GUI:  

`ctrl-alt-F3`  

## Open terminal  

`Super-T`

## Restore 'Legacy' icons

(application menus, including Dropbox, Jetbrains)

['Legacy' status icons](https://pop.system76.com/docs/status-icons/)

## Install pinyin roman characters with tone marks

```bash
sudo apt install ibus-m17n
sudo apt install ibus-pinyin
ibus restart
```

## Share Internet connection over Ethernet:

`nm-connection-editor`

## Force move file (vs copy)

drag while holding shift

## Recover sound from 'dummy output' (audio / headphones)

[Reference](https://www.linuxquestions.org/questions/linux-hardware-18/ubuntu-18-04-dummy-output-and-sound-disappeared-4175659386/)

```
killall pulseaudio
pulseaudio -k
```

---
title: "How to Setup Zoom on Linux with Wayland Session"
description: "Install Zoom and setup it on Linux with Wayland session."
summary: "Install Zoom and setup it on Linux with Wayland session."
date: 2024-01-21T02:01:11+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["zoom", "wayland", "troubleshooting", "teleconference", "guide", "linux", "tutorial"]
canonicalURL: ""
showToc: true
TocOpen: false
TocSide: 'right'  # or 'left'
# weight: 1
# aliases: ["/first"]
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
# UseHugoToc: true
cover:
    image: "images/cover.webp" # image path/url
    alt: "Cover: Zoom Logo" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/setup-zoom-linux-wayland/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Introduction

[Zoom](https://zoom.us/) is a video conferencing software that allows users to hold online meetings, training sessions, and webinars. It is available for Windows, macOS, Linux, iOS, and Android.

It is easy to install Zoom on Linux. However, if you are using a Wayland session, you may encounter some problems. In this article, I will show you how to install Zoom and setup it on Linux with Wayland session.

## Steps

### 1. Install Zoom

Download the latest Zoom package from [Zoom Download Center](https://zoom.us/download). Or you can get it from the Flatpak/Flathub repository.

### 2. Edit the Zoom Configuration File

Open the Zoom configuration file with your favorite text editor.

```bash
vim ~/.config/zoomus.conf
```

or if you are using Flatpak version of Zoom, open the configuration file with the following command.

```bash
vim ~/.var/app/us.zoom.Zoom/config/zoomus.conf
```

Add the following line to the file.

```bash
enableWaylandShare=true
enableMiniWindow=true
XDG_CURRENT_DESKTOP=gnome
```

For the other configuration options, please refer to [this thread](https://askubuntu.com/questions/1388053/what-are-all-of-the-available-zoomus-conf-options "What are all of the available zoomus.conf options? @ AskUbuntu").

![zoomus.conf](./images/zoomus_conf.webp#center)

> ⓘ Note: If you are using other desktop environments, you need to change the value of `XDG_CURRENT_DESKTOP` to the name of your desktop environment.

![Screenshare](./images/screenshare_wayland.webp#center)

### 3. Fix Custom Virtual Background

Zoom saves the default virtual backgrounds to `~/.zoom/data/VirtualBkgnd_Default`. If you are using a custom virtual background, you may encounter a problem that the background is not loaded correctly. To fix this problem, you need to copy the custom virtual background to `~/.zoom/data/VirtualBkgnd_Custom`.

![Copy the virtual background to `~/.zoom/data/VirtualBkgnd_Custom`](./images/VirtualBkgnd_Custom.webp#center)

![Select the virtual background](./images/VirtualBkgnd_Custom_2.webp#center)

![fixed virtual background](./images/VirtualBkgnd_Custom_3.webp#center)

## Conclusion

To use Zoom on Linux with Wayland session, you need to edit the Zoom configuration `zoomus.conf` to able Wayland share and mini window. If you are using a custom virtual background, you need to copy it to `~/.zoom/data/VirtualBkgnd_Custom`. That's all. Thank you for reading.

## References

- [AskUbuntu](https://askubuntu.com/questions/1388053/what-are-all-of-the-available-zoomus-conf-options "What are all of the available zoomus.conf options? - Ask Ubuntu")
- [Zoom Meetings @ Arch Linux Wiki](https://wiki.archlinux.org/title/Zoom_Meetings)
- [Zoom @ Flathub](https://flathub.org/apps/us.zoom.Zoom)
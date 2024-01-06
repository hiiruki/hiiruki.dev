---
title: "How to Fix Airspy SDR# No Device Selected Error"
description: "How to fix the Airspy SDR# No Device Selected error."
summary: "Troubleshooting the Airspy SDR# No Device Selected error."
date: 2024-01-06T07:28:21+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["SDRSharp", "Airspy", "SDR", "Troubleshooting", "RTL-SDR", "radio-frequency", "rtlsdr", "rtl2832", "SoftwareDefinedRadio"]
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
    alt: "Cover: SDR# No Device Selected Error" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/sdrsharp-no-device/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Introduction

[Airspy SDR#](https://airspy.com/download/) is a software-defined radio (SDR) application that can be used to receive radio signals. This application is developed by [Airspy](https://airspy.com/).

## Prerequisite

You must already configure the USB driver using [Zadig](https://zadig.akeo.ie/). You can follow the steps in the [RTL-SDR.com guide](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/).

## Steps

### 1. Download the missing DLL file

You can download the missing DLL file from [here](https://s.id/RTL-SDR-DLL). In this case, we only need the `rtlsdr.dll` file.

### 2. Copy the `rtlsdr.dll` file to the SDR# folder

Copy the `rtlsdr.dll` file to the SDR# folder. Ex: `/path/to/sdrsharp-x86/`

![Copy rtlsdr.dll](./images/copy-rtlsdr-dll.webp#center)

### 3. Configure the RTL-SDR device in SDR#

Click the hamburger menu (☰) in the top left corner of the SDR# window. Then, click the `Source` button. Choose `RTL-SDR USB` in the `Source` dropdown menu.

![Configure RTL-SDR device](./images/configure-rtl-sdr-device.webp#center)

Then choose `Generic RTL2832U OEM (0)` in the Device dropdown

![Configure RTL-SDR device](./images/device.webp#center)

### 4. Start the Airspy SDR# using the `play` button.

Press the `play` button to start listening to the radio signals.

![Start SDR#](./images/start-sdrsharp.webp#center)

## References

- [[SOLVED] : No device selected in SDRSharp program using SDR DVB-T+DVD+FM by Titof Abdellatif ANFLOUS @ YouTube](https://youtu.be/AN9GBDfy0W0?si=t3G0a3HeRdPnxOxU)
- [RTL-SDR Quick Start Guide](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/)
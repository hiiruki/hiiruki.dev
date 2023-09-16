---
title: "Updating the system time on the QRadar Console"
description: "Configure the system time on your QRadar® Console by setting the time manually, or by using NTP servers. The QRadar Console synchronizes its system time with the managed hosts in your deployment. "
summary: "Configure the system time on your QRadar® Console by setting the time manually, or by using NTP servers. The QRadar Console synchronizes its system time with the managed hosts in your deployment. "
date: 2023-09-16T17:09:14+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["qradar", "siem", "time", "ntp"]
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
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Overview

This guide describes how to configure the system time on your QRadar® Console by setting the time manually, or by using NTP servers. The QRadar Console synchronizes its system time with the managed hosts in your deployment.

## Steps

### 1. Click the Admin tab

- Click the hamburger menu (☰) in the top left corner of the QRadar Console.

![hamburger menu](./images/step1.webp#center "hamburger menu")

- Click **Admin**

![admin](./images/step1-2.webp#center "admin menu")

- Or you can just click the **Admin** tab

![admin tab](./images/step1-3.webp#center "admin tab")

### 2. In the System Configuration section, click the System and License Management icon.

![system and license management](./images/step2.webp#center "system and license management")

### 3. From the Display menu, select Systems.

Select the relevant host

![systems](./images/step3.webp#center "systems")

### 4. From the Actions menu, select View and Manage System, and then click the System Time tab.

![system time](./images/step4.webp#center "system time")

### 5. Select a time zone from the Time Zone menu.

You can configure only the time zone on a managed host. The system time is synchronized with the QRadar Console but if the managed host is in a different time zone, then you can change to that time zone.

![time zone](./images/step5.webp#center "time zone")

### 6. Set the time manually.

- Select the **Set time manually** check box.
- Change the **Date** and **Time** to the correct values.

![set time manually](./images/step6.webp#center "set time manually")

### 7. Set the time by using NTP servers.

- Select the **Specify NTP servers** check box.
- Clik the plus icon (**+**) to add an NTP server.
- You can use NTP server pools, such as `pool.ntp.org` or `time.google.com`.

![ntp servers](./images/step7.webp#center "ntp servers")

- The final result should look like this:

![ntp servers](./images/step7-2.webp#center "ntp servers")

- Click **Save**.

The first NTP server is the primary server. If the primary server is not available, the secondary server is used. If the secondary server is not available, the tertiary server is used. If the tertiary server is not available, the system time is not synchronized.

- If prompted to restart services, click **OK**.

![restart services](./images/step7-3.webp#center "restart services")

![restart services](./images/step7-4.webp#center "restart services")

## Conclusion

You have successfully configured the system time on your QRadar® Console by setting the time manually, or by using NTP servers. The QRadar Console synchronizes its system time with the managed hosts in your deployment.

## References

- [Updating the system time on the QRadar Console](https://www.ibm.com/docs/en/qsip/7.5?topic=configuration-update-system-time)
- [NTP Pool Project](https://www.ntppool.org/en/)
- [Google Public NTP](https://developers.google.com/time)
- [NTP Servers](https://www.ntppool.org/en/use.html)
- [NTP Servers in Asia](https://www.ntppool.org/zone/asia)
- [Indonesia NTP Servers](https://www.ntppool.org/zone/id)
- [NTP @ Wikipedia](https://en.wikipedia.org/wiki/Network_Time_Protocol "NTP @ Wikipedia")


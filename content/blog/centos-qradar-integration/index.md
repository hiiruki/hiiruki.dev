---
title: "Setup CentOS for IBM QRadar CE Integration with VMware Workstation"
description: ""
summary: "This a guide to setup CentOS for IBM QRadar CE Integration with VMware Workstation and send logs to QRadar CE."
date: 2023-09-12T16:15:51+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["centos", "qradar", "siem", "vmware", "linux", "security", "tutorial"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/centos-qradar-integration/"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Overview

This is a guide to setup CentOS for IBM QRadar CE Integration with VMware Workstation and send logs to QRadar CE.

CentOS in this setup will act as a client that will be monitored by QRadar CE.

## Prerequisites

- [VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html) or [VMware Workstation Player](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html)
- [QRadar CE ISO](https://www.ibm.com/community/qradar/ce/)

## Setup

> **Note:** Before you start, make sure your **QRadar CE VM** is **already running**.

### 1. Open VMware Workstation and click Open a Virtual Machine

![Open a Virtual Machine](./images/step1.webp#center "Open a Virtual Machine")

or you can click **File > Open...** or use the shortcut `Ctrl + O`

![Open a Virtual Machine](./images/step1-2.webp#center "Open a Virtual Machine")

### 2. Select the QRadar CE ISO file and click Open

![Select the QRadar CE ISO file](./images/step2.webp#center "Select the QRadar CE ISO file")

### 3. Name the VM and select the location to save the VM, then click Import

![Name the VM and select the location to save the VM](./images/step3.webp#center "Name the VM and select the location to save the VM")

### 4. Wait for the import to complete then click Edit virtual machine settings

![Wait for the import to complete](./images/step4.webp#center "Wait for the import to complete")

### 5. Change the virtual machine settings as needed

In my setup, I changed the following settings:

- Memory: 512 MB
- Processors: 1
- Network Adapter: NAT

> **Note:** We don't need that much memory and processors for this setup, because we will only use it as a dummy server/client. You can change the settings later if you need more memory and processors.

Change the memory from **6 GB** to **512 MB** (or as needed)

![memory](./images/step5.webp#center "memory")

Change the processors from **2** to **1** (or as needed)

![processors](./images/step5-2.webp#center "processors")

Change the network adapter from **Bridged** to **NAT**, then click **OK**

![network adapter](./images/step5-3.webp#center "network adapter")

So the final settings will be like this:

![final settings](./images/step5-4.webp#center "final settings")

### 6. Power on the VM

![Power on the VM](./images/step6.webp#center "Power on the VM")

### 7. Wait for the VM to boot up and login with the root user and create a new password

> **Note:** Don't forget the password that you created, because you will need it later.

![login with root user](./images/step7.webp#center "login with root user")

### 8. Configure the network

Type `nmtui` to open the Network Manager Text User Interface

![nmtui](./images/step8.webp#center "nmtui")

- Select **Set system hostname** and press **Enter**

![set system hostname](./images/step8-2.webp#center "set system hostname")

- Set the hostname, in my setup I set it to `centos` and press **Enter**

![set hostname](./images/step8-3.webp#center "set hostname")

- Select **OK** and press **Enter**

![select OK](./images/step8-4.webp#center "select OK")

- Select **Quit** and press **Enter**

![select Quit](./images/step8-5.webp#center "select Quit")

- type `clear` to clear the screen

- type `bash` to refresh the bash shell, so the hostname will be updated

![refresh bash shell](./images/step8-6.webp#center "refresh bash shell")

- Check the connection by typing `ping google.com` and press **Enter**

![ping google.com](./images/step8-7.webp#center "ping google.com")

- Check the IP address by typing `ip -br addr` and press **Enter**

> **Note:** Take note of the IP address, because you will need it later.

![ip -br addr](./images/step8-8.webp#center "ip -br addr")

In my case, the IP address is `192.168.211.128`

### 9. SSH to the VM centos

You can use [PuTTY](https://www.putty.org/), [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab), [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10), [MobaXterm](https://mobaxterm.mobatek.net/) or any other [SSH](https://en.wikipedia.org/wiki/Secure_Shell "SSH @ Wikipedia") client you want.

In my case, I use [Termius](https://termius.com/).

- Set the details as needed

![set the details](./images/step9.webp#center "set the details")

- Type `ssh root@<IP address>` and press **Enter**
- Type password that you created earlier and press **Enter**
- In Termius you can connect to the VM using **Quick Connect** feature, so you don't need to type the IP address and password every time you want to connect to the VM.

![ssh root@<IP address>](./images/step9-2.webp#center "ssh root@<IP address>")

- Voila! You are now connected to the VM

![connected to the VM](./images/step9-3.webp#center "connected to the VM")

### 10. Install the required packages and dependencies

- Type `yum install audit` and press **Enter**

![yum install audit](./images/step10.webp#center "yum install audit")

- Type `y` if prompted and press **Enter**

![y](./images/step10-2.webp#center "y")

### 11. Configure the auditd service

- Start the auditd service by typing `service start auditd` and press **Enter**
- If you get a warning, just type `systemctl daemon-reload` and press **Enter**
- Type `service start auditd` and press **Enter** again

![service start auditd](./images/step11.webp#center "service start auditd")

- Type `chkconfig auditd on` and press **Enter** to enable the auditd service

![chkconfig auditd on](./images/step11-2.webp#center "chkconfig auditd on")

- Type `service auditd status` and press **Enter** to check the status of the auditd service

![service auditd status](./images/step11-3.webp#center "service auditd status")

- If you encounter an error like this:

> The service command supports only basic LSB actions (start, stop, restart, try-restart, reload, force-reload, status). For other actions, please try to use systemctl.

![service auditd status error](./images/step11-4.webp#center "service auditd status error")

- Just type `systemctl start auditd` and press **Enter** to start the auditd service.

![systemctl start auditd](./images/step11-5.webp#center "systemctl start auditd")

### 12. Configure the audit rules

- Type `vi /etc/audisp/plugins.d/syslog.conf` and press **Enter** to edit the syslog.conf file

![vi /etc/audisp/plugins.d/syslog.conf](./images/step12.webp#center "vi /etc/audisp/plugins.d/syslog.conf")

![vi /etc/audisp/plugins.d/syslog.conf](./images/step12-2.webp#center "vi /etc/audisp/plugins.d/syslog.conf")

- Press `i` to enter the insert mode
- Change the content of the `syslog.conf` file to this:
    - active = yes
    - direction = out
    - path = builtin_syslog 
    - type = builtin
    - args = LOG_LOCAL6
    - format = string

- So the final content of the `syslog.conf` file will be like this:

![syslog.conf](./images/step12-3.webp#center "syslog.conf")

- Press `Esc` to exit the insert mode
- Type `:wq` and press **Enter** to save and exit the file

### 13. Configure the rsyslog service

- Type `vi /etc/rsyslog.conf` and press **Enter** to edit the rsyslog.conf file

![vi /etc/rsyslog.conf](./images/step13.webp#center "vi /etc/rsyslog.conf")

- Press `shift + G` to go to the end of the file
- Press `O` to enter the insert mode and add this line at the end of the file:
    - `*.* @<IP_ADDRESS_QRADAR>:514`
- Check the IP address of the QRadar CE VM, in my case the IP address is `192.168.211.129`

![rsyslog.conf](./images/step13-2.webp#center "rsyslog.conf")

- Like this:

![rsyslog.conf](./images/step13-3.webp#center "rsyslog.conf")

- Press `Esc` to exit the insert mode
- Type `:wq` and press **Enter** to save and exit the file

### 14. Restart the auditd and rsyslog services

- Type `service auditd restart` and press **Enter** to restart the auditd service

![service auditd restart](./images/step14.webp#center "service auditd restart")

- Type `systemctl restart rsyslog` and press **Enter** to restart the rsyslog service

![systemctl restart rsyslog](./images/step14-2.webp#center "systemctl restart rsyslog")

### 15. Open the QRadar CE Dashboard on your browser and add a filter

- Open your browser and go to `https://<IP_ADDRESS_QRADAR>`
- Login with the username `admin` and your password
- Click **Log Activity** and click **Add Filter**

![Log Activity](./images/step15.webp#center "Log Activity")

- Add a filter with the following details:
    - Parameter: `Source IP [Indexed]`
    - Operator: `Equals`
    - Value: `<IP_ADDRESS_CENTOS>`, in my case the IP address is `192.168.211.128`

![Add Filter](./images/step15-2.webp#center "Add Filter")

- Change the View to **Real Time (streaming)**

![Change the View](./images/step15-3.webp#center "Change the View")

### 16. Test the log with add user in the centos VM

- Type `useradd test` and press **Enter** to add a new user

![useradd test](./images/step16.webp#center "useradd test")

- If you get **Unknown log event**, you can restart the auditd and rsyslog services again
- Type `service auditd restart` and press **Enter** to restart the auditd service
- Type `systemctl restart rsyslog` and press **Enter** to restart the rsyslog service
- Type `useradd test` and press **Enter** again to add a new user
- Now you can see the activity log in the QRadar CE Dashboard
- You can also see the log in the `/var/log/audit/audit.log` file in the centos VM

![useradd test](./images/step16-2.webp#center "useradd test")

- Test deleting the user by typing `userdel test` and press **Enter**

![userdel test](./images/step16-3.webp#center "userdel test")

- Now you can see the activity log in the QRadar CE Dashboard, notice that the **Event Name** is contains user deletion activity.

![userdel test](./images/step16-4.webp#center "userdel test")

- You can try with other activities like `usermod`, `userpasswd`, `usergroup`, login and logout, change some configuration, etc.

![other activity](./images/step16-5.webp#center "other activity")

### 17. Voila! You have successfully setup CentOS for IBM QRadar CE Integration with VMware Workstation

You can now explore the QRadar CE Dashboard and see the logs from your CentOS VM.

## References

- https://www.ibm.com/community/qradar/ce/
- https://www.ibm.com/docs/en/SS42VS_7.4/pdf/b_siem_inst.pdf
- https://www.ibm.com/docs/en/SS42VS_7.4/pdf/b_qradar_system_notifications.pdf
- https://www.ibm.com/community/qradar/wp-content/uploads/sites/5/2020/03/QRadar_CE_Under_the_Radar_21Feb.pdf
- https://www.ibm.com/docs/en/qradar-on-cloud?topic=support-common-problems
- https://www.ibm.com/docs/en/qsip
- http://ftpmirror.your.org/pub/misc/ftp.software.ibm.com/software/security/products/qradar/documents/7.2.4/QLM/EN/b_qradar_system_notifications.pdf
- https://www.reddit.com/r/QRadar/comments/p5lfzz/best_strategy_for_monitor_linux_servers/
- [Forwarding Syslogs from Linux Hosts to QRadar](https://wiki.secure-iss.com/Public/SOC/LinuxLogForwarding)
- [Sending Linux logs to QRadar (rsyslog.conf) by Jose Bravo](https://youtu.be/Dmf2iwRqATI?si=Ctf9DJd9CHVp4sHk)
- [Mastering Linux OS Integration with IBM QRadar: A Comprehensive Guide to Supercharge Your Security” by Ahmad Hassan Tariq](https://medium.com/@AhmadCyberZone.com/mastering-linux-os-integration-with-ibm-qradar-a-comprehensive-guide-to-supercharge-your-security-9d1be9eab9c9)
- Guide/learning material from [Infinite Learning HCAI Program](https://kampusmerdeka.kemdikbud.go.id/program/studi-independen/browse/863c3409-8b4e-4c96-9edd-71ee61e9fc41/7a22d773-4ea0-11ed-a45a-c2cca2f5088a) (I can't share the material/content directly, because it's confidential and belong to [Infinite Learning](https://www.infinitelearning.id/) and IBM Academy)
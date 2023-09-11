---
title: "How to setup IBM QRadar CE on VMware Workstation"
description: ""
summary: "This is a guide to setup IBM QRadar Community Edition SIEM on VMware Workstation."
date: 2023-09-11T14:33:15+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["qradar", "siem", "vmware"]
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

This is a guide to setup IBM QRadar Community Edition SIEM on VMware Workstation.

IBM Qradar is a [security information and event management (SIEM)](https://en.wikipedia.org/wiki/Security_information_and_event_management "SIEM @ Wikipedia") product. It collects log data from an enterprise, its network devices, host assets and operating systems, applications, vulnerabilities, and user activities and behaviors. It also provides real-time monitoring, alerting, and offense management.

I use VMware® Workstation 17 Pro (17.0.0 build-20800274) and QRadar CE ISO (QRadarCE733GA_v1_0.ova).

**Software Requirements:**

- [VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html) or [VMware Workstation Player](https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html)
- [QRadar CE ISO](https://www.ibm.com/community/qradar/ce/)

**Hardware requirements:**

- Memory minimum requirements: 8 GB RAM or 10 GB w/applications
- Disk space minimum: 250 GB
- CPU: 2 cores (minimum) or 6 cores (recommended)
- One network adapter with access to the Internet is required
- A static public and private IP addresses is required for QRadar Community Edition
- The assigned hostname must be a fully qualified domain name

## Steps

### 1. Open VMware Workstation

![Open VMware Workstation Pro](./images/step1.webp#center "Open VMware Workstation Pro")

### 2. Click File > Open

![File > Open](./images/step2.webp#center "File > Open")

### 3. Select QRadar CE ISO (QRadarCE733GA_v1_0.ova) and click Open

![Select QRadar CE ISO](./images/step3.webp#center "Select QRadar CE ISO")

### 4. Name the VM and select the location to save the VM, then click Import

![Importing VM](./images/step4.webp#center "Importing VM")

### 5. Wait for the import to complete then click Memory under Devices

![Click Memory under Devices](./images/step5.webp#center "Click Memory under Devices")

### 6. Set the memory to 8 GB or 10 GB

> **Note:** If installation fails, try increasing the memory to 10 GB or more.

![Set the memory to 8 GB or 10 GB](./images/step6.webp#center "Set the memory to 8 GB or 10 GB")

### 7. Set the Processors to 2 cores (minimum) or 6 cores (recommended)

I set it to 4 cores.

![Set the Processors to 2 cores (minimum) or 6 cores (recommended)](./images/step7.webp#center "Set the Processors to 2 cores (minimum) or 6 cores (recommended)")

### 8. Set the Network Adapter from Bridged to NAT

![Set the Network Adapter from Bridged to NAT](./images/step8.webp#center "Set the Network Adapter from Bridged to NAT")

In VMware, the Bridged and NAT network adapter modes serve different purposes. Bridged mode allows the virtual machine (VM) to directly access the physical network as if it were a separate physical machine, receiving its own IP address and behaving as an independent device on the network. On the other hand, NAT (Network Address Translation) mode creates a private network within the host machine, allowing the VM to share the host's network connection. VMs in NAT mode use the host's IP address for external communication and are isolated from the external network, making them suitable for scenarios where the VMs need internet access but don't require direct interaction with external network devices.

For example, If you are in a Cafe and your VMs is not connected to the internet, try changing the Network Adapter from Bridged to NAT. This will allow your VMs to share the host's network connection.

Docs: [VMware Bridged vs NAT vs Host-Only Network](https://docs.vmware.com/en/VMware-Workstation-Pro/17/com.vmware.ws.using.doc/GUID-D9B0A52D-38A2-45D7-A9EB-987ACE77F93C.html)

### 9. When you are done with the settings, click Power on this virtual machine

![Power on this virtual machine](./images/step9.webp#center "Power on this virtual machine")

### 10. Wait for the VM to boot up, and then login with the root user and create a new password

> **Note:** Don't forget the password you set. You will need it later to login to the VM. Also, in linux when you type your password, it won't show anything. Just type it and press enter.

![Login with the root user and create a new password](./images/step10.webp#center "Login with the root user and create a new password")

### 11. Set the QRadar network settings to use IPv4 only

Type `nmtui` to open the Network Manager

![Type nmtui to open the Network Manager](./images/step11.webp#center "Type nmtui to open the Network Manager")

Wait for the NetworkManager TUI to open. Then select **Edit a connection** and press **Enter**

![select Edit a connection](./images/step11-2.webp#center "select Edit a connection")

Then select **Edit** using the arrow key and press **Enter**

![select Edit a connection](./images/step11-3.webp#center "select Edit a connection")

Set the **IPv6 configuration** to **Ignore** and press **Enter**

![Set the IPv6 configuration to Ignore](./images/step11-4.webp#center "Set the IPv6 configuration to Ignore")

So that it looks like this

![Set the IPv6 configuration to Ignore](./images/step11-5.webp#center "Set the IPv6 configuration to Ignore")

Then select **OK** and press **Enter**

### 12. Set the QRadar hostname

After setting the network settings, back to the main menu and select **Set system hostname** and press **Enter**

![Set system hostname](./images/step12.webp#center "Set system hostname")

Then type the hostname you want to use. For example `qradar.yourname.com` and choose **OK** then press **Enter**

![Set system hostname](./images/step12-2.webp#center "Set system hostname")

Docs: [Recommended practices for hostname creation](https://www.ibm.com/support/pages/qradar-recommended-practices-hostname-creation)

### 13. Reactivate the network settings

After setting the hostname, back to the main menu and select **Activate a connection** and press **Enter**

![Activate a connection](./images/step13.webp#center "Activate a connection")

Select the network interface and press **Enter**

Press **Enter** 2x in Deactivate option.

![change Deactivate to Activate](./images/step13-2.webp#center "change Deactivate to Activate")

### 14. Select Quit > OK and press Enter to save the changes

![Select OK and press Enter to save the changes](./images/step14.webp#center "Select OK and press Enter to save the changes")

### 15. Type `ls -l` to see the files in the current directory and type `./setup` to start the setup

![./setup](./images/step15.webp#center "./setup")

### 16. Accept the license agreement

Press **Enter** to accept the license agreement

![Press Enter to continue the setup](./images/step16.webp#center "Press Enter to continue the setup")

Press **Space** to scroll down

![Press Space to scroll down and type q to accept the license agreement](./images/step16-2.webp#center "Press Space to scroll down and type q to accept the license agreement")

and type `q` to accept the license agreement

![Press Space to scroll down and type q to accept the license agreement](./images/step16-3.webp#center "Press Space to scroll down and type q to accept the license agreement")

Then press **Enter** to continue

![Press Space to scroll down and type q to accept the license agreement](./images/step16-4.webp#center "Press Space to scroll down and type q to accept the license agreement")

### 17. Type `Y` to install the QRadar CE

![Type y to install the QRadar CE](./images/step17.webp#center "Type y to install the QRadar CE")

Wait for the installation to complete. This will take a while. Approximately 30 minutes to 1 hour or more. Depends on your internet connection and your computer specs.

![Wait for the installation to complete](./images/step17-2.webp#center "Wait for the installation to complete")

Mine took around 40 minutes to complete.

Rig:
- CPU: [Ryzen 5 4600H](https://www.amd.com/en/products/apu/amd-ryzen-5-4600h "Ryzen 5 4600H @ AMD") (6 cores, 12 threads)
- RAM: 16 GB (8GB dual channel)

![Finish installing](./images/step17-3.webp#center "Finish installing")

### 18. Set the password for the admin user to login to the QRadar CE web interface

Type the password you want to use and press **Enter**

> **Note:** Don't forget the password you set. You will need it later to login to the QRadar CE web interface. The password can be same as the VMs root password.

![Set the password for the admin user to login to the QRadar CE web interface](./images/step18.webp#center "Set the password for the admin user to login to the QRadar CE web interface")

### 19. Type `ip addr` or `ip a` to see the IP address of the VM

![Type ip addr or ip a to see the IP address of the VM](./images/step19.webp#center "Type ip addr or ip a to see the IP address of the VM")

Under the `ens33` interface, you will see the IP address of the VM. In my case, it's `192.168.211.128`.

> **Note:** The IP address of the VM will be different for everyone.

### 20. After we get the IP address, we can now SSH to the VM

You can use [PuTTY](https://www.putty.org/), [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab), [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10), [MobaXterm](https://mobaxterm.mobatek.net/) or any other [SSH](https://en.wikipedia.org/wiki/Secure_Shell "SSH @ Wikipedia") client you want.

In my case, I use [Termius](https://termius.com/).

- Open Termius and click **New Host**

![Open Termius and click New Host](./images/step20.webp#center "Open Termius and click New Host")

- Set the hostname to the IP address of the VM which is `192.168.211.128` and set the username to `root` and type the password you set earlier. You can also set the VM details if you want. In Termius you can set labels, groups, and tags to your VMs.

![setup hostname](./images/step20-2.webp#center "setup hostname")

- Connect to the VM

You can use the Quick Connect button to connect to the VM without having to type the IP address, username, and password.

![Connect to the VM](./images/step20-3.webp#center "Connect to the VM")

- Accept the fingerprint

Click **Add and continue**

![Accept the fingerprint](./images/step20-4.webp#center "Accept the fingerprint")

- You are now connected to the VM

![You are now connected to the VM](./images/step20-5.webp#center "You are now connected to the VM")

### 21. Check the Tomcat service status

Type `systemctl status tomcat` to check the Tomcat service status

Docs:
- [Tomcat Systemd](https://www.dogtagpki.org/wiki/Tomcat_Systemd "Tomcat Systemd Docs @ Dogtag PKI")
- [Tomcat Apache](https://tomcat.apache.org/tomcat-8.5-doc/index.html "Tomcat Docs @ Apache")

![Check the Tomcat service status](./images/step21.webp#center "Check the Tomcat service status")

### 22. Run this following command to update the QRadar CE

![Alert in IBM QRadar Website](./images/step22.webp#center "alert in IBM QRadar Website")

In the IBM QRadar CE ISO, there is a bug that prevents the QRadar CE from updating. QRadar developers has recently identified a defect in the product licensing function, which may cause the deployment to stop functioning. We need to run this following command.

More info: [UPDATED: A QRadar deploy changes on 31 December 2020 can impact product functionality](https://www.ibm.com/support/pages/node/6395080 "UPDATED: A QRadar deploy changes on 31 December 2020 can impact product functionality")

Copy and paste this command to the VM and press **Enter**

```bash
if [ -f /opt/qradar/ecs/license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/qradar/ecs/license.txt ; fi ; if [ -f /opt/ibm/si/services/ecs-ec-ingress/current/eventgnosis/license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/ibm/si/services/ecs-ec-ingress/current/eventgnosis/license.txt ; fi ; if [ -f /opt/ibm/si/services/ecs-ep/current/eventgnosis/license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/ibm/si/services/ecs-ep/current/eventgnosis/license.txt ; fi ; if [ -f /opt/ibm/si/services/ecs-ec/current/eventgnosis/license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/ibm/si/services/ecs-ec/current/eventgnosis/license.txt ; fi ; if [ -f /usr/eventgnosis/ecs/license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /usr/eventgnosis/ecs/license.txt ; fi ; if [ -f /opt/qradar/conf/templates/ecs_license.txt ] ; then echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/qradar/conf/templates/ecs_license.txt ; fi
```

<details>
<summary><b>Command break down</b></summary>

This is a complex shell command written in Bash scripting language. Let's break down what it does step by step:

1. `if [ -f /opt/qradar/ecs/license.txt ] ; then ... ; fi`:
   - This part of the command checks if a file named `license.txt` exists in the directory `/opt/qradar/ecs/`.
   - If the file exists, the subsequent command enclosed by `then` and `fi` is executed.

2. `echo -n "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20" > /opt/qradar/ecs/license.txt`:
   - If the file `/opt/qradar/ecs/license.txt` exists, this command overwrites the contents of that file with the given text: "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20".
   - The `-n` flag with `echo` is used to suppress the trailing newline character, so the text is written without a newline at the end.

The same logic is repeated for several other paths, checking for the existence of `license.txt` files and overwriting their contents if they exist. The paths being checked are as follows:

- `/opt/ibm/si/services/ecs-ec-ingress/current/eventgnosis/license.txt`
- `/opt/ibm/si/services/ecs-ep/current/eventgnosis/license.txt`
- `/opt/ibm/si/services/ecs-ec/current/eventgnosis/license.txt`
- `/usr/eventgnosis/ecs/license.txt`
- `/opt/qradar/conf/templates/ecs_license.txt`

In each case, if the respective `license.txt` file exists, it's overwritten with the same text: "QRadar:Q1 Labs Inc.:0007634bda1e2:WnT9X7BDFOgB1WaXwokODc:12/31/20".

This command seems to be updating license files for different components or services, ensuring that they all have the same license information. The provided information appears to be related to QRadar, likely a license key or information related to a software product.

</details><br>

![Run the command to update the QRadar CE](./images/step22-2.webp#center "Run the command to update the QRadar CE")

### 23. Open the QRadar CE web interface in your browser

Open your browser and type the IP address of the VM. In my case, it's `https://192.168.211.128`

> **Note:** Don't forget to use `https://` instead of `http://` because the QRadar CE web interface uses HTTPS.

- Click **Advanced...** and click **Accept the Risk and Continue**

![Click Advanced... and click Accept the Risk and Continue](./images/step23.webp#center "Click Advanced... and click Accept the Risk and Continue")

- Login with the username `admin` and the password you set earlier

![Login with the username admin and the password you set earlier](./images/step23-2.webp#center "Login with the username admin and the password you set earlier")

- Accept the EULA

![Accept the EULA](./images/step23-3.webp#center "Accept the EULA")

### 24. Configure the Network Activity

- Click the **breadcrumb**

![Click the breadcrumb](./images/step24.webp#center "Click the breadcrumb")

- Click **Admin**

![Click Admin](./images/step24-2.webp#center "Click Admin")

- Scroll down and click **Flow Sources**

![Click Flow Sources](./images/step24-3.webp#center "Click Flow Sources")

- Click **Add**

![Click Add](./images/step24-4.webp#center "Click Add")

- Wait for the form to load and set the **Flow Source Name** to `qradar_network` and set the **Flow Source Type** to `Network Interface` and click **Save**

![Set the Flow Source Name to qradar_network and set the Flow Source Type to Network Interface and click Save](./images/step24-5.webp#center "Set the Flow Source Name to qradar_network and set the Flow Source Type to Network Interface and click Save")

- So that it looks like this

![So that it looks like this](./images/step24-6.webp#center "So that it looks like this")

### 25. Deploy the changes

- Back to the admin page and click **Deploy Changes**

![Back to the admin page and click Deploy Changes](./images/step25.webp#center "Back to the admin page and click Deploy Changes")

- Click **Continue** if you are sure you want to deploy the changes

![Click Continue if you are sure you want to deploy the changes](./images/step25-2.webp#center "Click Continue if you are sure you want to deploy the changes") and wait for the changes to be deployed. This will take a while. Approximately 2-5 minutes or more.

### 26. Check the Network Activity tab, and if there are any logs, it means the QRadar CE is working

![Check the Network Activity tab, and if there are any logs, it means the QRadar CE is working](./images/step26.webp#center "Check the Network Activity tab, and if there are any logs, it means the QRadar CE is working")

## Congratulations! You have successfully setup IBM QRadar CE on VMware Workstation

## References:

- https://www.ibm.com/community/qradar/ce/
- https://www.ibm.com/docs/en/SS42VS_7.4/pdf/b_siem_inst.pdf
- https://www.ibm.com/docs/en/SS42VS_7.4/pdf/b_qradar_system_notifications.pdf
- https://www.ibm.com/community/qradar/wp-content/uploads/sites/5/2020/03/QRadar_CE_Under_the_Radar_21Feb.pdf
- https://www.ibm.com/docs/en/qradar-on-cloud?topic=support-common-problems
- https://www.ibm.com/docs/en/qsip
- http://ftpmirror.your.org/pub/misc/ftp.software.ibm.com/software/security/products/qradar/documents/7.2.4/QLM/EN/b_qradar_system_notifications.pdf
- Guide/learning material from [Infinite Learning HCAI Program](https://kampusmerdeka.kemdikbud.go.id/program/studi-independen/browse/863c3409-8b4e-4c96-9edd-71ee61e9fc41/7a22d773-4ea0-11ed-a45a-c2cca2f5088a) (I can't share the material/content directly, because it's confidential and belong to [Infinite Learning](https://www.infinitelearning.id/) and IBM Academy)

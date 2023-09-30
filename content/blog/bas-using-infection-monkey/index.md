---
title: "Breach and Attack Simulation (BAS) using Infection Monkey"
description: "The Infection Monkey is an open source security tool for testing a data center's resiliency to perimeter breaches and internal server infection. The Monkey uses various methods to self propagate across a data center and reports success to a centralized Monkey Island server."
summary: "The Infection Monkey is an open source security tool for testing a data center's resiliency to perimeter breaches and internal server infection. The Monkey uses various methods to self propagate across a data center and reports success to a centralized Monkey Island server."
date: 2023-09-29T11:40:41+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["infection-monkey", "breach-and-attack-simulation", "linux", "tutorial", "server", "security", "pentest", "penetration-testing", "bas", "monkey-island", "offensive-security", "cybersecurity", "red-team", "blue-team", "purple-team", "security-automation", "security-tools", " adversary-emulation", "infection-monkey"]
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
    alt: "Cover: Breach and Attack Simulation Workflow" # alt text
    caption: "Breach and Attack Simulation Workflow | [Dig8Labs](https://www.dig8labs.com/offensive-security/breach-and-attack-simulation/) " # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/bas-using-infection-monkey/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Introduction

Breach and Attack Simulation (BAS) is an advanced and state-of-the-art computer security testing method that helps identify vulnerabilities or loopholes in security environments and set-ups by mimicking the likely attack paths and techniques used by threat actors. It is a safe and controlled way to test the security posture of an organization and its ability to detect and respond to attacks. It is also known as a Purple Team exercise. The goal of BAS is to identify the gaps in the security posture of an organization and to provide actionable insights to improve the security posture. It is a continuous process and should be performed regularly to ensure that the security posture of an organization is up to date and can withstand the latest threats.

The [Infection Monkey](https://github.com/guardicore/monkey) is an open source security tool for testing a data center's resiliency to perimeter breaches and internal server infection. The Monkey uses various methods to self propagate across a data center and reports success to a centralized Monkey Island server. This is a great tool for testing the security of your network and servers. It is also a great tool for learning about network security and penetration testing.

The Monkey is consists of three components:

- Infection Monkey: Self propagation tool
- Monkey Island: Command and Control (C&C) server
- Monkey Business: Integrates with orchestration

![Monkey Components](./images/monkey_components.webp#center)

## Scenario

In this tutorial, we will use the Infection Monkey to test the security of a network. We will use the Monkey to infect a server and then use the Monkey to infect other servers on the network.

My setup is as follows:

- Kali Linux 2023.3 with Infection Monkey (Attacker) 
- CentOS 7 (Victim)
- IBM QRadar Community Edition (SIEM)

See the diagram below for a visual representation of the setup:

![Attack Diagram](./images/attack_diagram.webp#center)

## Steps

### 1. Install Infection Monkey

You can download the Infection Monkey from the [official website](https://www.guardicore.com/infectionmonkey/). You can also install it from the [GitHub repository](https://github.com/guardicore/monkey). The Infection Monkey is available for Windows, Linux, Docker, AWS, and Azure. In this case I downloaded the Linux version from the GitHub repository.

![Download Infection Monkey](./images/step1.webp#center)

Download the Infection Monkey AppImage from the GitHub repository:

```bash
wget https://github.com/guardicore/monkey/releases/download/v2.3.0/InfectionMonkey-v2.3.0.AppImage --no-check-certificate
```

![Download Infection Monkey AppImage](./images/step1-2.webp#center)

`--no-check-certificate` is used to bypass the SSL certificate check. This is useful if you are using a self-signed certificate.

### 2. Make the AppImage executable

Make the AppImage executable with the following command:

```bash
chmod u+x InfectionMonkey-v2.3.0.AppImage
```

chmod u+x is used to make the AppImage executable for the current user.

![Make the AppImage executable](./images/step2.webp#center)

### 3. Run the AppImage

Start Monkey Island by running the Infection Monkey AppImage package:

```bash
./InfectionMonkey-v2.3.0.AppImage
```

If you get errors related to FUSE, you may need to install FUSE 2.X first:

![FUSE error](./images/step3.webp#center)

```bash
sudo apt update
sudo apt install libfuse2
```

![Install FUSE 2.X](./images/step3-2.webp#center)

Docs: [Fuse Troubleshooting](https://docs.appimage.org/user-guide/troubleshooting/fuse.html)

> **Note:** If the error still occurs, you may need to redownload the AppImage it may be corrupted.

Then run the AppImage again:

```bash
./InfectionMonkey-v2.3.0.AppImage
```

![Run the AppImage](./images/step3-3.webp#center)

### 4. Access Infection Monkey web UI

Open your browser and go to `https://localhost:5000` to access the Infection Monkey web UI.

> **Note:** If you are using a self-signed certificate, you will get a warning message. Click on the Advanced button and then click on the Proceed to localhost (unsafe) link or click on the Accept the Risk and Continue button if you are using Firefox.

![Browser Warning](./images/step4.webp#center)

### 5. Register a new user

The account registration page will appear. Enter your username and password and click on the `Let's go!` button to register a new user.
This account will be used to log in to Monkey Island and to import/export Monkey Island configuration.

![Register a new user](./images/step5.webp#center)

Infection Monkey Dashboard

![Infection Monkey Dashboard](./images/step5-2.webp#center)

### 6. Configure the Infection Monkey

Click on the `Configuration` or `Configure Monkey` button to configure the Infection Monkey.

![Configure the Infection Monkey](./images/step6.webp#center)

You can configure the Propagation, Payloads, Credentials collectors, Masquerade, Polymorphism, Advanced, Exploiters, Network analysis, Credentials, and the General tab from the Configuration page. Configure the Infection Monkey according to your needs.

In this tutorial, we will configure the Infection Monkey to use the SSH Exploiter (Attempts a brute-force attack against SSH using known credentials, including SSH keys).

Enable the SSH Exploiter from the `Exploiters` tab.

![Configure the Infection Monkey](./images/step6-2.webp#center)

Configure the credentials from the `Credentials` tab. This will be used by the SSH Exploiter to brute-force the SSH server.

![Configure the Infection Monkey](./images/step6-3.webp#center)

You can enable the `Scan Agent's networks` from the `Network analysis` tab. This will allow the Infection Monkey to scan the network for other machines to infect.

![Configure the Infection Monkey](./images/step6-4.webp#center)

If the exploiter or the payload are not there, you can install them from the `Plugins` tab.

![Install Plugins](./images/step6-5.webp#center)

If you are done configuring the Infection Monkey, click on the `Submit` button to save the configuration.

### 7. Start the Infection Monkey

Go to the `Run Monkey` section and click on the `From Island` button to start the Infection Monkey to start the Monkey from the Monkey Island server.

![Start the Infection Monkey](./images/step7.webp#center)

Or you can run the Infection Monkey on other machines by clicking on the `Manual` button and selecting the operating system of the machine you want to run the Infection Monkey on.

Linux:

![Start the Infection Monkey on Linux](./images/step7-2.webp#center)

Windows:

![Start the Infection Monkey on Windows](./images/step7-3.webp#center)

### 8. View the Infection Map

Go to the `Infection Map` section to view the Infection Map.

![View the Infection Map](./images/step8.webp#center)

![View the Infection Map](./images/step8-2.webp#center)

You can see the Infection Map of the Infection Monkey. The Infection Monkey has infected the `CentOS 7` server and the `IBM QRadar Community Edition` server.

The network consists of 3 machines:

- Kali Linux 2023.3 with Infection Monkey (Attacker) with IP address `192.168.211.130`
- CentOS 7 (Victim) with IP address `192.168.211.128`
- IBM QRadar Community Edition (SIEM) with IP address `192.168.211.129`

> **Note:** The Windows machine shown in the Infection Map is not part of the network. It is ther

### 9. View the Events

Go to the `Events` section to view the Agent Events.

![View the Events](./images/step9.webp#center)

### 10. Monitor the Attack using a SIEM

In this tutorial, I will use IBM QRadar Community Edition as the SIEM. You can use other SIEMs such as Splunk, Elastic Stack, ArcSight, AlienVault, Azure Sentinel, etc.

![IBM QRadar Community Edition](./images/step10.webp#center)

You can see the Infection Monkey has infected the `CentOS 7` server and the `IBM QRadar Community Edition` server using the SSH Exploiter.

### 11. View the Security Reports

You can also export the Security Reports to a PDF file or print it.

![View the Security Reports](./images/step11.webp#center)

![View the Security Reports](./images/step11-2.webp#center)

## Conclusion

In this tutorial, we have learned how to use the Infection Monkey to test the security of a network. We have also learned how to use the Infection Monkey to infect a server and then use the Infection Monkey to infect other servers on the network.

The Infection Monkey is a great tool for testing the security of your network and servers. It is also a great tool for learning about network security and penetration testing.

Some of the advantages of using the Infection Monkey are:

1) Resilience testing
    - Simulates a real attacker
    - Propagate in-depth
2) Scale
    - "Pentester" in every VLAN
    - Full coverage
3) Automated tool
    - Continuous execution
    - Easy to use
4) Open source
    - Free
    - Community support
5) Integration
    - Monkey Business
    - Monkey Island API
6) Reporting
    - Security reports
    - Security events
7) Safe testing
    - Safely test your network or servers
    - The Infection Monkey is designed to be 100 percent safe, with no reconnaissance or propagation features that can impact server or network stability.

## References

- [Infection Monkey Documentation](https://techdocs.akamai.com/infection-monkey/docs/setting-up-infection-monkey)
- [Unleash the Infection Monkey: A Modern Alternative to Pen-Tests @ Black Hat USA 2016](https://youtu.be/M_kJ7zfAagc?si=OwghlC4wSKTG_7yB)
- [Making Breach & Attack Simulation Accessible and Actionable with Infection Monkey by Shay Nehmad @ Red Team Village](https://youtu.be/gOS1c375Hbg?si=iuuJ_5zhggbU4pm-)
- [Tutorial: Breach and Attack Simulation (BAS) with Infection Monkey by Semi Yulianto @ YouTube](https://youtu.be/ZJDAtFEI2g4?si=OimumknAtm6q5AHX)
- [Integrating Adversary Emulation using Infection Monkey with Azure Sentinel by Sartaj Ahmed Shaik @ Medium](https://tajsecguy.medium.com/integrating-adversary-emulation-using-infection-monkey-with-azure-sentinel-2ddf933a7af6)
- [Breach & Attack Simulation – What is that? by Priyank Gahlot @ LinkedIn](https://www.linkedin.com/pulse/breach-attack-simulation-what-priyank-gahlot)
- [Difference Between Breach and Attack Simulation(BAS), Red teaming, and VAPT by Raghav S. @ LinkedIn](https://www.linkedin.com/pulse/difference-between-breach-attack-simulationbas-red-teaming-raghav-som)
- [Automated Breach and Attack Simulation by Renier Steyn @ LinkedIn](https://www.linkedin.com/pulse/automated-breach-attack-simulation-renier-steyn)
- [Infection monkey - Automated Penetration Testing and Breach-Attack Simulation by Motasem Hamdan @ YouTube](https://youtu.be/qy6RqCPLV8Y?si=0m_U06ZP8UVThVFC)
- [Fuse Troubleshooting @ AppImage Docs](https://docs.appimage.org/user-guide/troubleshooting/fuse.html)
- [Breach and attack simulation (BAS) @ Wikipedia](https://en.wikipedia.org/wiki/Breach_and_attack_simulation)
- [Breach and Attack Simulation (BAS) @ dig8labs](https://www.dig8labs.com/offensive-security/breach-and-attack-simulation/)

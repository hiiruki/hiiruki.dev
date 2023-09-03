---
title: "[GSP101] Google Cloud Essential Skills: Challenge Lab"
description: ""
summary: "Quest: Cloud Architecture: Design, Implement, and Manage"
date: 2023-05-26T11:30:03+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["writeups", "challenge", "google-cloudskillsboost", "gsp101", "google-cloud", "cloudskillsboost", "juaragcp", "google-cloud-platform", "gcp", "cloud-computing", "cloud", "cloud-architecture"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/blob/main/writeups/GSP101/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

### GSP101

![Lab Banner](https://cdn.qwiklabs.com/GMOHykaqmlTHiqEeQXTySaMXYPHeIvaqa2qHEzw6Occ%3D)

- Time: 45 minutes
- Difficulty: Intermediate
- Price: 5 Credits

Lab: [GSP101](https://www.cloudskillsboost.google/focuses/1734?parent=catalog)<br>
Quest: [Cloud Architecture: Design, Implement, and Manage](https://www.cloudskillsboost.google/quests/124)<br>

🔄 Last updated: May 26, 2023

## Challenge scenario

Your company is ready to launch a brand new product! Because you are entering a totally new space, you have decided to deploy a new website as part of the product launch. The new site is complete, but the person who built the new site left the company before they could deploy it.

## Your challenge

Your challenge is to deploy the site in the public cloud by completing the tasks below. You will use a simple Apache web server as a placeholder for the new site in this exercise. Good luck!

1. Create a Compute Engine instance, add necessary firewall rules.

    - In the **Cloud Console**, click the **Navigation menu** > **Compute Engine** > **VM Instances**.
    - Click **Create instance**.
    - Set the following values, leave all other values at their defaults:

        | Property | Value (type value or select option as specified) |
        | --- | --- |
        | Name | `INSTANCE_NAME` |
        | Zone | `COMPUTE_ZONE` |

        ![Lab Variable](./images/lab_variable.webp#center)

        ![VM Create](./images/vm_create.webp#center)

    - Under **Firewall** check **Allow HTTP traffic**.

        ![Firewall](./images/firewall.webp#center)

    - Click **Create**.

2. Configure Apache2 Web Server in your instance.

    - In the **Cloud Console**, click the **Navigation menu** > **Compute Engine** > **VM Instances**.
    - Click on the SSH button next to `INSTANCE_NAME` instance.
    - Run the following command:

        ```bash
        sudo su -
        ```

        then run:

        ```bash
        apt-get update
        apt-get install apache2 -y

        service --status-all
        ```

3. Test your server.

    - In the **Cloud Console**, click the **Navigation menu** > **Compute Engine** > **VM Instances**.
    - Access the VM using an https address. Check that your URL is http:// EXTERNAL_IP and not https:// EXTERNAL_IP
    - Verify **Apache2 Debian Default Page** showed up.

## Congratulations!

![Congratulations Badge](https://cdn.qwiklabs.com/Ol0IAaeZbMNmToILKVne%2BkFlHoAu%2BZtH%2BErA8jO7m%2Bc%3D)

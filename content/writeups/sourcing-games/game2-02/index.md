---
title: "Game 2 – 02"
description: "https://sourcing.games/game-2/game-2-klvj9/"
summary: "Game 2 – 02"
date: 2024-02-27T19:07:31+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game2", "game2-2", "wayback-machine", "archive"]
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
    alt: "Cover: Sourcing Games Logo" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-02/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

I can’t travel back in time, but in October 26, 1996 on microsoft.com, I saw the name of the guy who became a certified trainer.

His name stuck in my mind, and that’s why this surname is the password for the next URL.

## Instructions

Type password: surname (lower case letters only)

## Solution

When dealing with a website and a look back in time, the first thing that comes to mind is the [Wayback Machine](https://archive.org/web/). I went to the website and entered the URL `microsoft.com` and selected the date `October 26, 1996`.

![Wayback Machine](images/wayback-machine.webp#center)

There are two snapshots available for this date and the first snapshot is captured with the time `16:45:56`.

I have no idea why the accessible snapshots are just one, but in wayback machine description there are two snapshots available. Anyway, I selected the first one and clicked on it.

![Wayback Machine Snapshots](images/wayback-machine-snapshots.webp#center)

When visiting the website, I found the name of the guy who became a certified trainer on bottom of the page.

Which is `Robert McIntosh`

![Robert McIntosh](images/robert-mcintosh.webp#center)

Based on the instructions, the password is the surname and it should be in lower case letters only. So, the password is `mcintosh`.

## Flag/Password

<details>
<summary> Show </summary>

`mcintosh`

</details>

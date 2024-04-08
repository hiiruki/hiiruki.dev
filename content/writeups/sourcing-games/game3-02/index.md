---
title: "Game 3 – 02"
description: "https://sourcing.games/game-3/game-3-d7sdf/"
summary: "Game 3 - 02"
date: 2024-04-07T23:12:33+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game3", "game3-2", "binary"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game3-02/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Sometimes, you need to decode messages that people are sharing on their profile.
Because you can use that info in the message that you are going to send them.

01010000 01100001 01110011 01110011 01110111 01101111 01110010 01100100 00100000 01101001 01110011 00111010 00100000 01110011 01110100 01100001 01100011 01101011 00110001 00110100

## Instructions

Use the right password

## Solution

The message is in binary. You can use an online tool to convert it to text.

I used [Cryptii](https://cryptii.com/pipes/binary-decoder) to convert the binary to text. You can use any other tool you like.

The decoded message is:

```plaintext
Password is: stack14
```

![binary](images/binary.webp#center)

## Flag/Password

<details>
<summary> Show </summary>

`stack14`

</details>

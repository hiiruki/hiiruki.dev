---
title: "Game 1 – 05"
description: "https://sourcing.games/game-1/game-1-k1vs1/"
summary: "Game 1 – 05"
date: 2024-02-26T15:40:46+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "SOCMINT", "stackoverflow", "twitter", "github", "sourcing-games", "game1", "game1-05"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game1-05/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Find the first name of this [StackOverflow user](https://meta.stackoverflow.com/users/5696502/arsen).

## Instructions

Password is the first name.

(Example: John)

## Solution

Visit the [StackOverflow user](https://meta.stackoverflow.com/users/5696502/arsen) profile.

Check if the user has any social media accounts linked to the profile. In this case, the user has a [Twitter (𝕏)](https://twitter.com/ArSiHaSi) and [GitHub](https://github.com/ArSn) account linked to the profile.

![StackOverflow](images/stackoverflow.webp#center)

- [GitHub](https://github.com/ArSn) account

![GitHub](images/github.webp#center)

- [Twitter (𝕏)](https://twitter.com/ArSiHaSi) account

![Twitter](images/twitter.webp#center)

We can see that the user's first name is shown in the both accounts. Which is `Kolja`. With the full name being `Kolja Zuelsdorf`. With this information, we can use `Kolja` as the password.

> Tips: Always check other linked accounts for additional information of the target or person of interest (PoI).

## Flag/Password

<details>
<summary> Show </summary>

`Kolja`

</details>

---
title: "Game 1 – 03"
description: "https://sourcing.games/game-1/game-1-h4xgm/"
summary: "Game 1 – 03"
date: 2024-02-08T22:58:11+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game1", "game1-03", "shorturl", "bitly"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game1-03/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Find the date when this URL (shortener) was created.

Password is Month and Day (eg. “jan” and day “1”)

https://bit.ly/mylnkbio

## Instructions

If you are checking for the right date, try to use incognito mode.

Type password: month-day<br>
Example: jan-4 (all lower case)

## Solution

The URL is shortened using [Bitly](https://bitly.com/) and when we open it, it redirects us to a [Jan Tegze](https://www.linkedin.com/in/jantegze/)'s LinkedIn profile.

![Jan Tegze's LinkedIn profile](images/Jan_Tegze_Linkedin.webp#center)

A quick search on the internet and we can find that Bitly has a feature to see the creation date of a shortened URL. We can add a `+` at the end of the URL to see the statistics of the shortened URL. Source: [Stack Overflow](https://stackoverflow.com/questions/41802729/how-to-find-out-date-in-which-url-was-shortened)

![stackoverflow](images/stackoverflow.webp#center)

So the URL becomes https://bit.ly/mylnkbio+ and we can see the creation date of the shortened URL.

![Bityly date](images/bitly_date.webp#center)

As we can see, the creation date of the shortened URL is April 17, 2020 16:18 UTC

## Flag/Password

<details>
<summary> Show </summary>

`apr-17`

</details>

---
title: "Game 1 – 02"
description: "https://sourcing.games/game-1/game-1-csa7a/"
summary: "Game 1 – 02"
date: 2024-02-08T21:36:11+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game1", "game1-02", "reverse-image-search"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game1-02/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Find who is this person and his name will unlock another level.

![Photo](images/photo.jpg#center)

<p align=center> <a href="https://sourcing.games/wp-content/uploads/2017/03/photo-203x300.jpg" title="photo-203x300.jpg">Open in a new tab</a> </p>

## Instructions

Password is: surname (lower case letters only)

## Solution

The image is a photo of a person. We can use reverse image search to find the person's name. For the reverse image search, I used an extension called "[Search by Image](https://github.com/dessant/search-by-image)" by [Armin Sebastian](https://armin.dev/). The extension allows me to search the image on multiple search engines at once. Currently, it supports [Google](https://images.google.com/), [Bing](https://www.bing.com/visualsearch), [Yandex](https://yandex.com/images/), [Baidu](https://image.baidu.com/), [Sogou](https://pic.sogou.com/), [TinEye](https://tineye.com/), [Shutterstock](https://www.shutterstock.com/images), and [Alamy](https://www.alamy.com/). The extension is available for [Firefox](https://addons.mozilla.org/firefox/addon/search_by_image/), [Chrome](https://chrome.google.com/webstore/detail/search-by-image/cnojnbdhbhnkbcieeekonklommdnndci), [Edge](https://microsoftedge.microsoft.com/addons/detail/search-by-image/hckehkfhdkpmdlonmjaagiodlpjbonmc), [Opera](https://addons.opera.com/extensions/details/search-by-image/), Safari for [iOS](https://apps.apple.com/us/app/search-by-image-for-safari/id1544552106?platform=iphone) and [macOS](https://apps.apple.com/us/app/search-by-image-for-safari/id1544552106?platform=mac), and also [Samsung Internet](https://galaxystore.samsung.com/detail/dev.armin.searchbyimage).

1. Right-click the image and select "Search by Image". The extension will open multiple search engines with the image. In this case, I used Bing images.

![Right-click and select Search by Image](images/search-by-image.webp#center)

![Search by Image](images/bing.webp#center)

2. The search results show that the person in the photo is [Todd Boyce](https://www.imdb.com/name/nm0101668/) (born July 1, 1961) is an American actor. He is known for his role as Stephen Reid in the ITV soap opera Coronation Street (1996–1997, 2007, 2022–2023). Reference: [Wikipedia](https://en.wikipedia.org/wiki/Todd_Boyce)

![Todd Boyce](images/Todd-Boyce.webp#center)

## Flag/Password

<details>
<summary> Show </summary>

`boyce`

</details>

---
title: "Game 2 – 01"
description: "https://sourcing.games/game-2/game-2-hnm7m/"
summary: "Game 2 – 01"
date: 2024-02-27T10:22:16+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game2", "game2-1", "url"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-01/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Get the password from the URL below.

[Open URL](https://www.sourcing.%20games/games/02s/)

## Instructions

Type password from URL

## Solution

When I clicked the link, I got an error message `This site can’t be reached`. Turns out the URL is incorrect because of some extra space in the URL.

The incorrect URL is `https://www.sourcing. games/games/02s/`. The correct URL should be `https://www.sourcing.games/games/02s/`.

![button](images/button.webp#center)

In [Chrome](https://www.google.com/intl/en/chrome/), the space is encoded as `%20` and the web is can't be reached.

![Page Error](images/page-error.webp#center)

I removed the space in the URL and the page is loaded correctly.

`https://www.sourcing.%20games/games/02s/` &#8594; `https://www.sourcing.games/games/02s/`

The page contains the password for the challenge.

![Password](images/password.webp#center)

When using [Firefox](https://www.mozilla.org/en-US/firefox/browsers/), somehow you can't click the button because that broken URL. You can inspect the element and remove the space in the URL to get the correct URL.

![Inspect Element](images/inspect-element.webp#center)

## Flag/Password

<details>
<summary> Show </summary>

`4vc7sa`

</details>

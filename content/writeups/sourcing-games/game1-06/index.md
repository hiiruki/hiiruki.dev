---
title: "Game 1 – 06"
description: "https://sourcing.games/game-1/game-1-ku7xa/"
summary: "Game 1 – 06"
date: 2024-02-26T16:30:46+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game1", "game1-06", "opendir", "directory-listing"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game1-06/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

One folder of this website “[inovace.eu](https://inovace.eu/)” was indexed by Google.

You can find there the password for the next level.

## Instructions

Use the password from the site

## Solution

Based on the description, some folder of the website `inovace.eu` was indexed by Google and maybe has [directory listing](https://probely.com/vulnerabilities/directory-listing) enabled.

But I'm curious about the website, so I'll visit it first.

![homepage](images/homepage.png)

Turns out, the website is under construction. So, let's find the directory.

To find the directory, we can use the following Google dork:

```plaintext
site:inovace.eu
```

![google-dork](images/google-dork.png)

or

```plaintext
index of site:inovace.eu
```

![google-dork2](images/google-dork2.png)

Well that was easy. The result shows the password in google search result. The password is `007games` which in the `/folder` directory (https://inovace.eu/folder/).

![password](images/password.png)

Well the website also has directory listing enabled. So, let's visit the directory.

![directory](images/dir-listing.png)

in the directory, there are 3 files which are:

- [`resume.docx`](files/resume.docx)

![resume.docx](images/resume-docx.png)

- [`resume.pdf`](files/resume.pdf)

![resume.pdf](images/resume-pdf.png)

- [`start.html`](files/start.html)

![start.html](images/start-html.png)

The file `resume.docx` and `resume.pdf` both contain password `kxas71`. But, when I tried to use the password, it didn't work. So, I tried the password from `/folder` directory, and it worked. So, the password is `007games`.

The `kxas71` password either is a _red herring_ or for another level.

And we finished the first Sourcing Game! 🎉

![congrats](images/congrats.png "https://sourcing.games/game-1/game-1-fs7ff/")

## Flag/Password

<details>
<summary> Show </summary>

`007games`

</details>

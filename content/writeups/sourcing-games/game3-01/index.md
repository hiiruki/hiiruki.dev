---
title: "Game 3 – 01"
description: "https://sourcing.games/game-3/game-3-pof4q/"
summary: "Game 3 - 01"
date: 2024-04-07T21:32:43+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game3", "game3-1", "directory-listing", "opendir"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game3-01/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

Get the password from the URL below.

[Open URL](http://g3.inovace.eu/start.html)

## Instructions

Type password from URL

## Solution

Visiiting the provided URL, we see a page called `start.html` with the content:

![start.html](images/start.webp#center)

Try visiting the home page of the website, http://g3.inovace.eu/, we see a [directory listing](https://portswigger.net/kb/issues/00600100_directory-listing):

![Directory Listing](images/dir-listing.webp#center)

The files in the directory are:

- [`resume.pdf`](files/resume.pdf)
- [`resume.docx`](files/resume.docx)
- `start.html`

Opening the `resume.pdf` and `resume.docx` file, we see the following content:

`resume.pdf`:
![resume.pdf](images/resume-pdf.webp#center)

`resume.docx`:
![resume.docx](images/resume-docx.webp#center)

Ater opening the `resume.pdf` and `resume.docx` file, we can see the password in the content.

## Flag/Password

<details>
<summary> Show </summary>

`kxas71`

</details>

## References

- https://portswigger.net/kb/issues/00600100_directory-listing
- https://cwe.mitre.org/data/definitions/548.html

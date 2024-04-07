---
title: "Game 2 – 07"
description: "https://sourcing.games/game-2/game-2-csda7d/"
summary: "Game 2 – 07"
date: 2024-02-29T14:17:19+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game2", "game2-7", "docx", "metadata", "libreoffice", "xml", "password", "microsoft-word"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-07/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

__THIS IS NOT THE END. ONE MORE URL AND YOU WILL FINISH THE GAME!__

## Attachments

- [Download File](https://sourcing.games/games/02s/one-more-url.docx "one-more-url.docx")
- [Mirror](files/one-more-url.docx "one-more-url.docx")

## Instructions

Use password from file.

_If you are Mac user, maybe it’s time to call your friends with Windows. They have more experience with Word. 😉_

## Solution

### LibreOffice Writer

There a file named `one-more-url.docx` and we should use the password from the file to continue the game.

Opening the file, we only see a single smile emoji. In this case I use LibreOffice Writer to open the file because I'm using Linux.

![Smile Emoji Docx](images/smile-emoji-docx.webp#center "Smile Emoji Docx")

Since the content is only a smile emoji, I suspect that there is something hidden in the file or there is something in the metadata.

So I look the document properties in LibreOffice Writer by clicking `File` > `Properties`.

![File](images/file-menu.webp#center "File")

In `General` tab there is nothing interesting other than creation date that created on `12/13/2016`, `15:34:00` and the author is `@jantegze` with hashtag `#SourcingGames`. But it is not the password/flag.

![Properties General](images/properties-general.webp#center "Properties General")

Then I go to `Description` tab and there is a `Title` with value `Interesting, right? :)`. But it is not the password/flag.

![Properties Description](images/properties-description.webp#center "Properties Description")

Then I go to `Custom Properties` tab and there is a `Company` with value `42sourcer`.

![Properties Custom](images/properties-custom.webp#center "Properties Custom")

I try to use `42sourcer` as the password and it works.

### Microsoft Word

You can simply right-click the file and choose `Properties` > `Details` tab.

![File Properties Details](images/file-properties.webp#center "File Properties Details")

Also if you are using Microsoft Word, you can open the file and go to `File` > `Info` > `Properties` > `Advanced Properties` > `Summary` tab. Also you can just click the `Show All Properties` button.

![Word Properties Advanced](images/word-info-properties.webp#center "Word Properties Advanced")

## Flag/Password

<details>
<summary> Show </summary>

`42sourcer`

</details>

## References

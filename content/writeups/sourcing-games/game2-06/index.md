---
title: "Game 2 – 06"
description: "https://sourcing.games/game-2/game-2-cas74/"
summary: "Game 2 – 06"
date: 2024-02-29T13:13:31+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "SOCMINT", "sourcing-games", "game2", "game2-6", "linkedin", "google-dorking", "google-fu", "google-dork", "dorking", "google-hacking"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-06/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

***THINK LOCALLY, ACT LOCALLY!***

In 2016, I met a great guy, who worked as a Developer in Poland, not sure if he was from Warsaw, Wroclaw or Crakow. But what I remember was that he is a developer (intermediate level), working with Angular, Java, JUnit and Python.

When he told me his name I thought that he was a foreigner, but he doesn’t speak a word in English, only Polish.
I also found his LinkedIn profile, I hope he will learn English and I wish I was fluent in Polish.

## Instructions

You can use his name as a password for another level. (Lower case letters only)

Example: john-doe  (first name-surname)

## Solution

Based on the description, we need to find a developer from Poland who works with Angular, Java, JUnit, and Python. The developer's location is unknown, but it could be Warsaw, Wroclaw, or Crakow and he doesn't speak English. Also he has a LinkedIn profile.

The developer's name will be used as a password for the next level.

So, because we don't have the developer's name, we need to find it first. We can use some google-fu or google dorking to find the developer's LinkedIn profile.

Here are my search queries:

```plaintext
Developer Angular, Java, JUnit, Python Warsaw, Wroclaw, Crakow site:linkedin.com
```

I'm just using the keywords from the description and adding `site:linkedin.com` to limit the search results to LinkedIn only.

![Google Dork](images/google-dork.webp#center)

The first result is a developer named `Petr Davis`. Let's check his LinkedIn profile.

![LinkedIn Profile](images/linkedin-profile.webp#center)

The experience section shows that he is a developer (Deweloper / Programista) from Cracow, Lesser Poland District, Poland and he has worked with Angular, Java, JUnit, and Python for 8 yrs 2 mos (Jan 2016 - Present). Nb: as the date of this writeup written.

![Experience](images/experience.webp#center)

The profile is likely matching the description. Let's use `petr-davis` as the password for the next level.

And it's correct! We're lucky that the first result is the correct one. If it's not, we need to check the other results and compare the details with the description.

## Flag/Password

<details>
<summary> Show </summary>

`petr-davis`

</details>

## References

- [GoogleDorking.md by sundowndev @ GitHub Gist](https://gist.github.com/sundowndev/283efaddbcf896ab405488330d1bbc06)
- [Google Dorking Cheat Sheet by chr3st5an @GitHub](https://github.com/chr3st5an/Google-Dorking)
- [Download Google Dorks Cheat Sheet PDF for Quick References by hackr.io](https://hackr.io/blog/google-dorks-cheat-sheet) - [Download](https://drive.google.com/file/d/1EdbKbdP3Tfkj1zBQ4NICLwnvzcM-bX9g/view "Hackr.io’s Google Dorks Cheat Sheet PDF.pdf") - [Mirror](files/Hackr.io’s%20Google%20Dorks%20Cheat%20Sheet%20PDF.pdf "Hackr.io’s Google Dorks Cheat Sheet PDF.pdf")
- [Google Dorking Hacking and Defense Cheat Sheet by SANS Institute](https://www.sans.org/posters/google-hacking-and-defense-cheat-sheet/) - [Download](https://sansorg.egnyte.com/dl/f4TCYNMgN6) - [Mirror](files/GoogleCheatSheet.pdf "GoogleCheatSheet.pdf")
- [Google hacking @ Wikipedia](https://en.wikipedia.org/wiki/Google_hacking)

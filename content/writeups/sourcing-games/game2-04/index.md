---
title: "Game 2 – 04"
description: "https://sourcing.games/game-2/game-2-c4cca/"
summary: "Game 2 – 04"
date: 2024-02-27T20:28:19+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "sourcing-games", "game2", "game2-4", "robots.txt", "linkedin"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-04/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

LinkedIn disallows all robots to index some things, and these robots already know that your “keyword for next level” is a part of the e-mail address before @linkedin.com.

## Instructions

Password is the keyword before @linkedin.com

## Solution

The hint is about `robots.txt` file. The `robots.txt` file is a text file webmasters create to instruct web robots (typically search engine robots) how to crawl pages on their website. The `robots.txt` file is part of the the [Robots Exclusion Protocol](https://en.wikipedia.org/wiki/Robots_exclusion_standard) (REP), a group of web standards that regulate web robot behavior. The REP is not a standard, but a convention.

The `robots.txt` file is a simple text file placed on a website's server that tells webcrawlers which pages or files the crawler can or can't request from your site. This is used mainly to avoid overloading your site with requests; it is not a mechanism for keeping a web page out of Google. To keep a web page out of Google, you should use noindex directives, or password-protect your page.

So, let's check the `robots.txt` file of the LinkedIn website. The `robots.txt` file is located at the root of the website, so we can access it by visiting https://www.linkedin.com/robots.txt

Based on the hint, we are looking for an e-mail address. Specifically, we are looking for the keyword before `@linkedin.com`. We can use the `Ctrl + F` to search for `@linkedin.com` and find the keyword.

![robots.txt](images/robots-txt.webp#center)

From the `robots.txt` file, we can see that the e-mail address is `whitelist-crawl@linkedin.com`. But the password is the keyword before `@linkedin.com`. So, the password is `whitelist-crawl`.

<br>

> **Note**: The `robots.txt` file is a public file and is not meant to be hidden. It is used to instruct web robots how to crawl pages on the website. It is not a security measure and should not be used to store sensitive information.

> **Note**: The level 3 of the game is not available at the time of writing this writeup. Because after solved the 2nd level, the next level is 4th level. So, I assume that the 3rd level is not available.

## Flag/Password

<details>
<summary> Show </summary>

`whitelist-crawl`

</details>

## References

- [Introduction to robots.txt](https://developers.google.com/search/docs/crawling-indexing/robots/intro)
- [What is a robots.txt file?](https://moz.com/learn/seo/robotstxt)
- [What is robots.txt? | How a robots.txt file works](https://www.cloudflare.com/learning/bots/what-is-robots-txt/)
- [robots.txt @ Wikipedia](https://en.wikipedia.org/wiki/Robots.txt)
- [The ultimate guide to robots.txt](https://yoast.com/ultimate-guide-robots-txt/)
- [The Web Robots Pages](https://www.robotstxt.org/)

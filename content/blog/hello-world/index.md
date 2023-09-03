---
title: "Hello World!"
description: "Yet another blog."
summary: "Yet another blog."
date: 2023-09-03T21:48:44+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["random", "misc", "hello-world", "SSG"]
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
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/blob/main/writeups/GSP101/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

![Hello World!](images/hello-world.gif#center "Hello World in terminal")

Yeah, my another blog ~~again~~ (￢_￢)

Previously I had a blog that used Static Site Generator (SSG) which is [Eleventy](https://11ty.dev), but now I have moved to other SSGs and what I'm using now is [Hugo](https://gohugo.io/).

## Tech Stack

- [Hugo](https://gohugo.io/) for the Static Site Generator (SSG)
- [Netlify](https://netlify.com) to host this site and for the CI/CD pipeline
- [GitHub](https://github.com) to host the source code

## Why SSG?

I'm using SSG because it's easier to use and it's faster than using CMS (Content Management System) like [WordPress](https://wordpress.com/). I don't need to worry about the server, database, etc. I just need to write the content and the SSG will generate the static site for me.

Static site generators offer several advantages that make them a compelling choice:

- ***Efficiency***: SSGs pre-generate web pages, eliminating the need for server-side processing. This results in faster load times and reduced server resource consumption.
- ***Security***: Since there's no dynamic server-side code execution, the attack surface is smaller, making your website less vulnerable to security threats.
- ***Scalability***: Static sites can handle high levels of traffic without performance issues, making them suitable for projects of all sizes.
- ***Version Control***: Content and code can be easily managed with version control systems like Git, enabling collaborative development and content updates.
- ***Cost-Effectiveness***: Hosting static sites is often less expensive than dynamic sites because you don't need robust server infrastructure or database management.
- ***Simplicity***: SSGs encourage a straightforward development process. Content is created and organized in plain text files (e.g., Markdown), and the generator takes care of rendering them into HTML.
- ***Portability***: You can host static sites on a variety of platforms, making it easy to switch hosting providers or migrate your site.
- ***Maintainability***: Easy to maintain regarding software updates.
- ***Transparency***: Transparent in what is going on under the hood. Especially the open-source SSGs.

## Why Hugo?

I'm using Hugo because it's fast, simple, and easy to use. It's also written in Go, making it cross-platform. I'm avoiding the use of Node.js because it's bloated and slow. Additionally, some individuals have [security concerns related to JavaScript](https://yewtu.be/watch?v=pid5kmWXSj8), so I'm minimizing its usage as much as possible. This site also functions properly even when JavaScript is disabled.

## Why Netlify?

I'm using Netlify because it's free, easy to use, and it has a CI/CD pipeline. I'm using the free plan because I don't need the paid plan yet. I'm also using Netlify because it's easy to set up and it's easy to connect to GitHub.

## Why Blogging?

I started this blog to jot down things I've learned, mainly because I tend to forget stuff I picked up earlier. But hey, I've made it public, so you're welcome to give it a read and pick up things too. Sharing is caring, after all! ^^

Sorry if there are any mistakes in the blog/articles/writeups, you can [contact](/about/#contacts) me if you have any questions.

Anyway, welcome to my blog and happy reading! ^^

![Thank You!](images/sailor-saturn.webp#center 'Hotaru "Sailor Saturn, Guardian of Silence" Tomoe from Sailor Moon')

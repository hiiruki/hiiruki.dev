---
title: "Game 2 – 05"
description: "https://sourcing.games/game-2/game-2-cjas1/"
summary: "Game 2 – 05"
date: 2024-02-28T08:22:42+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["OSINT", "SOCMINT", "sourcing-games", "game2", "game2-5", "github", "email", "docx"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/writeups/sourcing-games/game2-05/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Description

The first part of the e-mail address of this [GitHub user](https://github.com/angularjs-gdit) is the password that will open the file below. (Use only the part before @)
The password that is in that file will open the next level.


NOTE: DO NOT contact this GitHub user for any hints or your account/IP will be blocked!

## Attachments

🗎 [Download File](https://sourcing.games/games/02s/githubuser.docx "githubuser.docx")

🗎 [Mirror](files/githubuser.docx "githubuser.docx")

## Instructions

Type password from the file.

## Solution

So we have to find the first part of the e-mail address of the GitHub user [angularjs-gdit](https://github.com/angularjs-gdit) in order to open the password-protected Microsoft Word document (docx) file.

Visiting the GitHub profile, we can see the user is not displaying their e-mail address in the profile section.

![GitHub Profile](images/github-profile.webp#center)

The next step is to search the e-mail address of the user in the public repos, commits, issues, and pull requests.

I found one interesting repository, [angularjs-gdit/slideshow](https://github.com/angularjs-gdit/slideshow), which contains a PowerPoint presentation file (pptx) named [`angularjs.pptx`](files/angularjs.pptx). But, no e-mail address was found in the file.

![pptx](images/pptx.webp#center)

When I checked the commits of the latest repository, also no e-mail address was found in the commit messages. Usually some developers sign their commits with their e-mail address using the `-s` flag (e.g. `git commit -s -m "commit message"`) these features are using GPG keys to sign the commits.

![commits](images/commits.webp#center)

I also checked the issues and pull requests, but no e-mail address was found.

Then, I remembered that GitHub has a feature that allows users to check commit patches. So to view the patch of the latest commit, I visited the latest commit page and added `.patch` at the end of the URL.

https://github.com/angularjs-gdit/example-01-helloworld/commit/4243528ac995e2bb717eed82b06fea620ab7f0f2.patch

![patch](images/patch.webp#center)

And there it is, the e-mail address of the user is `pt103368@PT103368.corp.int`. But we only need the first part of the e-mail address, which is `pt103368`.

Another way to find the e-mail address is by using the `git log` command. First, clone the repository using the following command.

```bash
git clone https://github.com/angularjs-gdit/example-01-helloworld.git
```

![git clone 1](images/git-clone1.webp#center)

![git clone 2](images/git-clone2.webp#center)

Then navigate to the cloned repository

```bash
cd example-01-helloworld
```

and use the following command to view the commit history.

```bash
git log
```

![git log 1](images/git-log1.webp#center)

or to view it in a specific format, you can use the following command.

```bash
git log --pretty=format:"%h %an %ae" -1
```

![git log 2](images/git-log2.webp#center)

The command above will display the commit hash, author name, and author e-mail address of the latest commit.

So we got the first part of the e-mail address, which is `pt103368`. Now we can use it to open the password-protected Microsoft Word document (docx) file.

![docx](images/docx.webp#center)

When the file is opened, we can see the password to open the next level.

## Extras

For GitHub OSINT stuff I made a script/tools to automate the process, you can find it [here](https://github.com/hiiruki/ghosint). It's called `ghosint` which the name is coming from "GitHub OSINT". It's a simple Python script that uses the GitHub API to gather information about a user or an organization. This tools requires a GitHub API token to work.

The information that can be gathered are:

- User Information:
  - Username
  - Name
  - ID
  - Node ID
  - Gravatar ID
  - Location
  - Bio
  - Email
  - Twitter
  - Company
  - Hireable
  - Organizations
  - Followers
  - Following
  - Type
  - Created at
  - Updated at

- Repo Information
  - Public Repos
  - Public Gists
  - GitHub Gist

- Screenshots

![ghosint](images/ghosint.webp#center)

For more information about the script, you can visit the [GitHub repository](https://github.com/hiiruki/ghosint).

## Flag/Password

<details>
<summary> Show </summary>

`s00rcing`

</details>

## References

- [A list of cool features of Git and GitHub by Justin Garrison @ GitHub](https://git.io/sheet)
- [Most commonly used git tips and tricks by git-tips @ GitHub](https://git.io/git-tips)
- [GitHub URL Hacks by Justin Garrison](https://justingarrison.com/blog/2021-07-11-github-url-hacks/)
- [Hack GitHub! Find Anyone's Email with this Simple Trick! by Brian Lagunas @ YouTube](https://youtu.be/s_HEnfbpBg8?si=hi3gh9SUI-m_-rgh)

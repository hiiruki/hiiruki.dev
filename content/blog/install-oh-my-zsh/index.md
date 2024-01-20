---
title: "How to Install ZSH and Oh My ZSH on Linux"
description: "Install ZSH and Oh My ZSH on Linux."
summary: "Install ZSH and Oh My ZSH on Linux."
date: 2024-01-20T09:52:21+07:00
draft: false
author: "Hiiruki" # ["Me", "You"] # multiple authors
tags: ["zsh", "oh-my-zsh", "linux", "terminal", "shell", "bash"]
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
    alt: "Cover: Oh My ZSH Logo" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/install-oh-my-zsh/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Introduction

[ZSH](https://en.wikipedia.org/wiki/Z_shell "zsh @ Wikipedia") or Z shell is a shell designed for interactive use, although it is also a powerful scripting language. Many of the useful features of [bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) "bash @ Wikipedia"), [ksh](https://en.wikipedia.org/wiki/KornShell "ksh @ Wikipedia"), and [tcsh](https://en.wikipedia.org/wiki/Tcsh "tcsh @ Wikipedia") were incorporated into zsh; many original features were added.

[Oh My Zsh](https://ohmyz.sh/) is an open source, community-driven framework for managing ZSH configuration. It comes bundled with thousands of helpful functions, helpers, plugins, themes, and many more.

In this article, I will show you how to install ZSH and Oh My ZSH on Linux.

## Steps

### 1. Install ZSH

Install with default package manager.

- __Debian/Ubuntu__

```bash
sudo apt install zsh
```

- __Fedora/CentOS/RHEL__

```bash
sudo dnf install zsh
```

- __Arch Linux__

```bash
sudo pacman -S zsh
```

### 2. Install Oh My ZSH

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 3. Change Default Shell to ZSH

```bash
sudo chsh -s $(command -v zsh)
```

### 4. Install Plugins

- __Fast Syntax Highlighting (F-Sy-H)__

    Feature rich syntax highlighting for Zsh.

```bash
git clone --depth 1 https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

- __zsh-autosuggestions__

    _[Fish](http://fishshell.com/)-like fast/unobtrusive autosuggestions for zsh._

    It suggests commands as you type based on history and completions.

    Requirements: Zsh v4.3.11 or later

```bash
git clone --depth 1 https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

- __zsh-completions__

    Additional completion definitions for [Zsh](https://www.zsh.org/).

```bash
git clone --depth 1 https://github.com/zsh-users/zsh-completions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions
```

### 5. Configure ZSH and Oh My ZSH

Edit `~/.zshrc` file.

```bash
nano ~/.zshrc
```

> ⓘ NOTE
> <br>Use your preferred text editor.

Configure `themes` and `plugins`.

- __Plugins__

```bash
plugins=(
        git
        bgnotify
        zsh-autosuggestions
        zsh-completions
        fast-syntax-highlighting
)
```

> ⓘ NOTE
> - `git` is a default plugin. It is used to display the current git branch, git information, and other useful git-related workflow.
> - `bgnotify` is a default plugin. It is used to notify you when a background job completes.

- __Themes__

```bash
ZSH_THEME="agnoster"
```

> ⓘ NOTE
> <br>You can find more themes [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes).
> <br>For the external themes, you can find them [here](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes).

- __Other Configurations (Optional)__

- Speeds up pasting when using zsh-autosuggestions

```bash
# Speeds up pasting when using zsh-autosuggestions.
# See "https://github.com/zsh-users/zsh-autosuggestions/issues/238".
paste_init()
{
    OLD_SELF_INSERT="${${(s.:.)widgets[self-insert]}[2,3]}"
    zle -N self-insert url-quote-magic
}
paste_done()
{
    zle -N self-insert "$OLD_SELF_INSERT"
}
zstyle :bracketed-paste-magic paste-init paste_init
zstyle :bracketed-paste-magic paste-finish paste_done
```

- Case-insensitive completion

```bash
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
```

### 6. Restart ZSH

You can restart ZSH by closing and opening the terminal or by running the following command.

```bash
exec zsh
```

## References

- [ZSH](https://www.zsh.org/)
- [Oh My ZSH](https://ohmyz.sh/)

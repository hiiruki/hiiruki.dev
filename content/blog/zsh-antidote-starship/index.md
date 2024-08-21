---
title: "Setting up ZSH with Antidote and Starship"
description: "Setup ZSH with Antidote and Starship prompt"
summary: "Setup ZSH with Antidote and Starship prompt"
date: 2024-08-22T00:08:31+07:00
draft: false
author: "Hiiruki"
tags: ["zsh", "antidote", "starship", "shell", "prompt", "linux", "terminal"]
showToc: true
TocOpen: false
TocSide: 'right'
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
    alt: Cover image" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/zsh-antidote-starship/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Intro

So basically, [ZSH](https://en.wikipedia.org/wiki/Z_shell "ZSH @Wikipedia") is a shell, [Antidote](https://getantidote.github.io/) is a plugin manager for ZSH, and [Starship](https://starship.rs/) is a prompt.

For a long time, I had always used [oh-my-zsh](https://ohmyz.sh/) for my ZSH configuration, but recently, I noticed that it was a bit slow in my terminal. After doing some research, I found out that Antidote is a faster alternative to oh-my-zsh. I decided to give it a try, and I'm happy with the result.

You can check Roman's ZSH benchmark [here](https://github.com/romkatv/zsh-bench/blob/master/doc/linux-desktop.md).

## Steps

### Install ZSH

Install ZSH using your package manager. For Arch Linux, you can use the following command:

```bash
sudo pacman -S zsh
```

Change the default shell to ZSH:

```bash
sudo chsh -s $(command -v zsh)
```

![](./images/1.webp#center)

If your default shell is still `/bin/bash`, you can restart your system or log out and log back in.

Here I successfully changed the default shell to ZSH:

![](./images/2.webp#center)

### Install Antidote

First, clone the Antidote to the `~/.antidote` directory:

```bash
git clone --depth=1 https://github.com/mattmc3/antidote.git ${ZDOTDIR:-~}/.antidote
```

Then, add the following lines to your `~/.zshrc`:

```zsh
# source antidote
source ~/.antidote/antidote.zsh

# initialize plugins statically with ${ZDOTDIR:-~}/.zsh_plugins.txt
antidote load
```

#### Plugins File

You can create a file named `~/.zsh_plugins.txt` to list the plugins you want to load.

```bash
nano ~/.zsh_plugins.txt
```

and add the plugins you want to load. For example:

```txt
# .zsh_plugins.txt - comments begin with "#"

# Basic Zsh plugins are defined in user/repo format
jeffreytse/zsh-vi-mode

# Bash plugins may also work
rupa/z

# empty lines are skipped

# annotations are also allowed:
romkatv/zsh-bench kind:path
olets/zsh-abbr    kind:defer

# set up Zsh completions with plugins
mattmc3/ez-compinit
zsh-users/zsh-completions kind:fpath path:src

# frameworks like oh-my-zsh are supported
getantidote/use-omz        # handle OMZ dependencies
ohmyzsh/ohmyzsh path:lib   # load OMZ's library
ohmyzsh/ohmyzsh path:plugins/colored-man-pages  # load OMZ plugins
ohmyzsh/ohmyzsh path:plugins/magic-enter

# or lighter-weight ones like zsh-utils
belak/zsh-utils path:editor
belak/zsh-utils path:history
belak/zsh-utils path:prompt
belak/zsh-utils path:utility

# prompts:
#   with prompt plugins, remember to add this to your .zshrc:
#   `autoload -Uz promptinit && promptinit && prompt pure`
sindresorhus/pure     kind:fpath
romkatv/powerlevel10k kind:fpath

# popular fish-like plugins
mattmc3/zfunctions
zsh-users/zsh-autosuggestions
zdharma-continuum/fast-syntax-highlighting kind:defer
zsh-users/zsh-history-substring-search
```

After saving the file, close and reopen your terminal or run `source ~/.zshrc` to apply the changes.

![](./images/3.webp#center)

#### Load the Plugins (MANUAL/OPTIONAL)

> ⓘ NOTE
> <br>This is for the manual update for the static plugins

**You can skip this step if you followed the recommended install procedure.**

If you followed the recommended install procedure, your plugins will already be loaded when you called antidote load in your .zshrc.

However, you could choose generate your static plugins file manually with antidote bundle. Basically, antidote will only need to run when you change your .zsh_plugins.txt file.

You can generate the static plugins file with the following command:

```bash
# generate ~/.zsh_plugins.zsh
antidote bundle <~/.zsh_plugins.txt >~/.zsh_plugins.zsh
```

We can run the command at any time to update the static plugins file. However, if you followed the recommended install procedure you won’t need to do this yourself.

Finally, the static generated plugins file gets sourced in your .zshrc.

```zsh
# .zshrc
source ~/.zsh_plugins.zsh
```

Note that to use antidote bundle this way, we will never want to call antidote init. Be sure that’s not in your ~/.zshrc. antidote init is a wrapper provided for backwards compatibility for users familiar with antibody and antigen, but is no longer recommended.

### Install Starship

Before installing Starship, you need to install a [Nerd Font](https://www.nerdfonts.com/) and enabled in your terminal (for example,try the [FiraCode Nerd Font](https://www.nerdfonts.com/font-downloads)).

In Arch Linux you can install the FiraCode Nerd Font simply by using the following command:

```bash
sudo pacman -S ttf-fira-code
```

![](./images/4.webp#center)

Then, install Starship using the following command:

```bash
curl -sS https://starship.rs/install.sh | sh
```

Or you can use the package manager to install Starship. For Arch Linux, you can use the following command:

```bash
sudo pacman -S starship
```

![](./images/5.webp#center)

#### Set up the shell to use Starship

In this case we are using ZSH, so add the following line to your `~/.zshrc`:

```zsh
eval "$(starship init zsh)"
```

#### Configure Starship 

Start a new shell session and you should see the cool Starship prompt. If you're happy with the defaults, enjoy! If you want to customize it, you can configure Starship by editing the `~/.config/starship.toml` file.

```yaml
# Get editor completions based on the config schema
"$schema" = 'https://starship.rs/config-schema.json'

# Inserts a blank line between shell prompts
add_newline = true

# Replace the '❯' symbol in the prompt with '➜'
[character] # The name of the module we are configuring is 'character'
success_symbol = '[➜](bold green)' # The 'success_symbol' segment is being set to '➜' with the color 'bold green'

# Disable the package module, hiding it from the prompt completely
[package]
disabled = true
```

If you're looking to further customize Starship:

- [Configuration](https://starship.rs/config/) – learn how to configure Starship to tweak your prompt to your liking
- [Presets](https://starship.rs/presets/) – get inspired by the pre-built configuration of others

## Quick Benchmark

### Vanilla ZSH

![](./images/6.webp#center)

### With Antidote and Starship

![](./images/7.webp#center)

## Summary

I found that Antidote is faster than oh-my-zsh, and Starship is a cool, fast prompt written in Rust that gets updated frequently. While there are many other prompt alternatives like Powerlevel10k, I prefer Starship because it's simple and fast. Some people might prefer Powerlevel10k because it has a transient prompt feature, and I've heard it's faster than Starship. However, I also use Powerlevel10k, and I've found that the performance gap is not that significant. I plan to write a post comparing Starship and Powerlevel10k in the future.

## References

- [Antidote Documentation](https://getantidote.github.io/)
- [zsh-bench by @romkatv (Roman Perepelitsa)](https://github.com/romkatv/zsh-bench/blob/master/doc/linux-desktop.md)
- [How to fix slow zsh shell startup by Dane Harnett Devs @ YouTube](https://www.youtube.com/watch?v=I_EaA7Q3GxI)
- [Supercharge your terminal by Insanet](https://insanet.eu/post/supercharge-your-terminal/)
- [Speeding Up My Shell (Oh My Zsh) by Matthew J. Clemente](https://blog.mattclemente.com/2020/06/26/oh-my-zsh-slow-to-load/)
- [Dev Workstation Setup](https://jobs.narrative.io/process/dev-workstation-setup/)
- [Does anyone have the list of plugin for antidote plugin manager project? @ Reddit](https://www.reddit.com/r/zsh/comments/1b8uezw/does_anyone_have_the_list_of_plugin_for_antidote/)
- [zsh-bench](https://github.com/romkatv/zsh-bench)

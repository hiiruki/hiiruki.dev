---
title: "Enable Wayland on GNOME with NVIDIA GPU in Arch Linux"
description: "How to enable Wayland on GNOME with NVIDIA GPU in Arch Linux"
summary: "How to enable Wayland on GNOME with NVIDIA GPU in Arch Linux"
date: 2024-08-16T23:35:03+07:00
draft: false
author: "Hiiruki"
tags: ["arch-linux", "arch", "gnome", "wayland", "nvidia", "xorg", "x11", "gdm", "display-server"]
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
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/enable-wayland-gnome-nvidia-arch-linux/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Intro

Recently, I've installed [Arch Linux](https://archlinux.org/) on my laptop with [GNOME](https://www.gnome.org/) as the desktop environment. But I noticed that it was using [Xorg](https://x.org/wiki/) as the display server instead of [Wayland](https://wayland.freedesktop.org/). So I decided to switch to Wayland with [NVIDIA GPU](https://www.nvidia.com/en-eu/geforce/gaming-laptops/gtx-1650/). Here's how I did it.

## My System

- Laptop: [ASUS TUF Gaming A15 (FX506IH)](https://www.asus.com/laptops/for-gaming/tuf-gaming/asus-tuf-gaming-a15/)
- OS: [Arch Linux x86_64](https://archlinux.org/)
- Kernel: [Linux 6.10.5-zen1-1-zen](https://github.com/zen-kernel/zen-kernel/releases/tag/v6.10.5-zen1)
- DE: [GNOME 46](https://release.gnome.org/46/)

## Steps

### Kernel Mode Setting (KMS)

#### Configuration

Kernel mode setting (KMS) is a method for setting display resolution and depth in the [kernel space](https://en.wikipedia.org/wiki/User_space_and_kernel_space "User space and kernel space @ Wikipedia") rather than [user space](https://en.wikipedia.org/wiki/User_space_and_kernel_space "User space and kernel space @ Wikipedia")). It can be used in conjunction with the [framebuffer](https://en.wikipedia.org/wiki/Linux_framebuffer "Linux Framebuffer @ Wikipedia") device. KMS also enables newer technologies (such as [DRI2](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure "DRI @ Wikipedia")) which will help reduce artifacts and increase 3D performance, even kernel space power-saving.

> ⓘ NOTE:<br>
> At first, note that for any method you use, you should always disable:<br>
> - Any **vga=** options in your bootloader as these will conflict with the native resolution enabled by KMS.<br>
> - Any **video=** lines that enable a framebuffer that conflicts with the driver.<br>
> - Any other framebuffer drivers (such as uvesafb).<br>

Because I generated the grub config using the `grub-mkconfig` tool and have the default configuration, I don't have the `vga=` or `video=` neither drivers that make conflicts with native resolution enabled by KMS. So, I'm good to go.

#### Late KMS start

[Intel](https://wiki.archlinux.org/title/Intel), [Nouveau](https://wiki.archlinux.org/title/Nouveau), [ATI](https://wiki.archlinux.org/title/ATI) and [AMDGPU](https://wiki.archlinux.org/title/AMDGPU) drivers already enable KMS automatically for all chipsets, but the proprietary [NVIDIA](https://wiki.archlinux.org/title/NVIDIA) driver does not. To enable KMS for the NVIDIA driver, we need to [manually enabled](https://wiki.archlinux.org/title/NVIDIA#DRM_kernel_mode_setting) it.

#### DRM kernel mode setting

To enable it, set the `modeset=1` [kernel module parameter](https://wiki.archlinux.org/title/Kernel_module_parameter) for the `nvidia_drm` module.

```bash
sudo nano /etc/default/grub
```

Edit the `GRUB_CMDLINE_LINUX_DEFAULT` line to include `nvidia-drm.modeset=1`:

![](./images/etc-default-grub.webp#center)

Save the file and regenerate the grub config:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

in my case the path is `/boot/efi` so the command will be:

```bash
sudo grub-mkconfig -o /boot/efi/grub/grub.cfg
```

![](./images/grub-mkconfig.webp#center)

#### Early KMS start (Optional)

KMS is typically initialized after the [initramfs](https://en.wikipedia.org/wiki/Initial_ramdisk) stage. However, it is possible to enable KMS already during the initramfs stage. Add the required module for the video driver to the initramfs configuration file:

`nvidia` `nvidia_modeset` `nvidia_uvm` `nvidia_drm` for the out-of-tree [nvidia](https://archlinux.org/packages/?name=nvidia) and [nvidia-open drivers](https://archlinux.org/packages/?name=nvidia-open). 

#### mkinitcpio

Configure the `mkinitcpio` to include the NVIDIA modules:

```bash
sudo nano /etc/mkinitcpio.conf
```

Add the `nvidia` `nvidia_modeset` `nvidia_uvm` `nvidia_drm` modules to the `MODULES` array:

![](./images/mkinitcpio-conf.webp#center)

Save and regenerate the initramfs using `mkinitcpio`, because I'm using the [linux-zen](https://github.com/zen-kernel/zen-kernel/wiki/FAQ) kernel, so the command will be:

```bash
sudo mkinitcpio -p linux-zen
```

Make sure to replace `linux-zen` with your kernel name. Like `linux`, `linux-lts`, `linux-hardened`, etc. You can check the kernel name using the `uname -r` command.

![](./images/mkinitcpio.webp#center)

For the full kernel list you can check in Arch Wiki [Kernel](https://wiki.archlinux.org/title/Kernel) page.

or you can use the `-P` flag to regenerate all preset file in `/etc/mkinitcpio.d` directory:

```bash
sudo mkinitcpio -P
```

#### pacman hook

To ensure that the initramfs is always updated when the NVIDIA driver is updated, create a [pacman hook](https://wiki.archlinux.org/title/NVIDIA#pacman_hook) that will regenerate the initramfs automatically.

First, create the hook directory:

```bash
sudo mkdir -p /etc/pacman.d/hooks
```

Then create the hook file:

```bash
sudo nano /etc/pacman.d/hooks/nvidia.hook
```

Paste the following content:

```bash
[Trigger]
Operation=Install
Operation=Upgrade
Operation=Remove
Type=Package
# Uncomment the installed NVIDIA package
Target=nvidia
#Target=nvidia-open
#Target=nvidia-lts
# If running a different kernel, modify below to match
Target=linux-zen

[Action]
Description=Updating NVIDIA module in initcpio
Depends=mkinitcpio
When=PostTransaction
NeedsTargets
Exec=/bin/sh -c 'while read -r trg; do case $trg in linux*) exit 0; esac; done; /usr/bin/mkinitcpio -P'
```

Make sure to edit the `Target` line to match your NVIDIA driver package and kernel name. In my case, I'm using the `nvidia` package and `linux-zen` kernel.

![](./images/nvidia_hook.webp#center)

### Install GNOME (If you haven't)

```bash
sudo pacman -S gnome
```

In selection prompt, just press `Enter` to install all the packages. (default=all)

### GDM Configuration

#### /etc/gdm/custom.conf (Optional)

If you want to use Wayland as the default session, you can edit the `/etc/gdm/custom.conf` file:

```bash
sudo nano /etc/gdm/custom.conf
```

Uncomment the `WaylandEnable` line and set it to `true`:

![](./images/gdm-custom-conf.webp#center)

#### Symlink the gdm rules

This step is often skipped that will cause the GDM only to use Xorg. To fix this, you need to symlink the GDM rules:

```bash
sudo ln -s /dev/null /etc/udev/rules.d/61-gdm.rules
```

![](./images/symlink.webp#center)

### Reboot

After all the steps above, reboot your system:

```bash
sudo reboot
```

### Check

After rebooting in the login screen, you can check if you're using Wayland by clicking the gear icon and see if there's a `GNOME on Wayland` or just `GNOME` but the old one is `GNOME on Xorg`.

You can also check the XDG_SESSION_TYPE environment variable:

```bash
echo $XDG_SESSION_TYPE
```

Also you can check the about section in the settings.

Like this:

![](./images/before_after.webp#center)

You can use tools like `neofetch`, `screenfetch` or `fastfetch` to check the NVIDIA GPU.

```bash
fastfetch
```

![](./images/fastfetch.webp#center)

## Summary

Now you have successfully enabled Wayland on GNOME with NVIDIA GPU in Arch Linux. You can check the [References](#references) for more information.

## References

- [Wayland @ ArchWiki](https://wiki.archlinux.org/title/Wayland)
- [Kernel mode setting @ ArchWiki](https://wiki.archlinux.org/title/Kernel_mode_setting)
- [NVIDIA DRM KMS @ ArchWiki](https://wiki.archlinux.org/title/NVIDIA#DRM_kernel_mode_setting)
- [GDM @ ArchWiki](https://wiki.archlinux.org/title/GDM#Wayland_and_the_proprietary_NVIDIA_driver)
- [NVIDIA @ ArchWiki](https://wiki.archlinux.org/title/NVIDIA)
- [GNOME @ ArchWiki](https://wiki.archlinux.org/title/GNOME)
- [Wayland on Arch Linux (with Nvidia proprietary driver) by s1n7ax @ YouTube](https://youtu.be/_YtgszmnfN8?si=i6L1W2kax2C-CDps)
- [DRI @ Wikipedia](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure)
- [Linux Framebuffer @ Wikipedia](https://en.wikipedia.org/wiki/Linux_framebuffer)
- [User space and kernel space @ Wikipedia](https://en.wikipedia.org/wiki/User_space_and_kernel_space)


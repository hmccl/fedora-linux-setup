# Fedora Workstation 42 Setup

This is a guide to setup Fedora Workstation 42.

## First boot

Upgrade the system. Wait for 5 minutes (in case of a kernel update) and reboot.

```bash
sudo dnf upgrade
```

These are useful `dnf` commands.

```bash
sudo dnf autoremove
sudo dnf clean all
dnf history list
```

## RPM Fusion

RPM Fusion is a repository that contains free and nonfree software.
Follow the documentation. Look up NVIDIA and Multimedia Howtos.

## Flathub

Enable the Flathub remote. Follow the documentation.

## Snap

Install `snapd`. Follow the documentation.

## Packages

Remove and install packages.

```bash
sudo dnf remove rhythmbox
sudo dnf install dconf-editor gnome-builder decibels gnome-extensions-app gnome-music epiphany sqlitebrowser
sudo dnf install git fish fd-find ripgrep fzf gcc clang cmake luarocks nodejs sqlite neovim vim texlive-scheme-basic texlive-babel-portuges pandoc sile sil-gentium-plus-fonts alerque-libertinus-fonts texlive-tex-gyre texlive-tex-gyre-math source-foundry-hack-fonts levien-inconsolata-fonts langpacks-pt_BR
flatpak install flathub app.zen_browser.zen com.brave.Browser org.gnome.World.PikaBackup org.keepassxc.KeePassXC org.squidowl.halloy
sudo snap install codium --classic google-cloud-sdk --classic typst vlc
```

## fish

Change the login shell to fish.

```
sudo usermod --shell /usr/bin/fish $USER
```

## dconf

Change `dconf` options.

```
dconf write /org/gnome/desktop/input-sources/xkb-options ['ctrl:nocaps']
dconf write /org/gnome/shell/app-picker-layout []
```

## Configuration files

- `.gitconfig`
- `config.fish`
- `.vimrc`
- `init.lua`
- `.boto`

# Fedora 41 KDE Plasma Setup

This is a guide to setup Fedora 41 KDE.

## First boot

Upgrade the system. Wait for 5 minutes (in case of a kernel update) and reboot.

```
sudo dnf upgrade
```

These are useful `dnf` commands.

```
sudo dnf autoremove
dnf clean all
dnf history list
```

## RPM Fusion

RPM Fusion is a repository that contains free and nonfree software.

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
sudo dnf update @core
```

### NVIDIA

Upgrade the system and install NVIDIA drivers.

```
sudo dnf upgrade
sudo dnf install akmod-nvidia
```

Wait for 5 minutes (see `top`) and reboot.

Run `modinfo -F version nvidia` to see the version of the driver.

### Multimedia

Install multimedia codecs.

```
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
```

### Hardware acceleration

Install Intel media driver.

```
sudo dnf install intel-media-driver
```

Reboot.

## Flathub

Enable the Flathub remote.

```
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Snap

Install snapd.

```
sudo dnf install snapd
```

Log out.

```
sudo ln -s /var/lib/snapd/snap /snap
```

Log out again.

## Packages

Remove and install packages.

```
sudo dnf remove kmahjongg kmines kpat akregator kde-connect kmail krdc krfb ktnef pim-data-exporter dragon kaddressbook kontact korganizer kgpg kmouth
sudo dnf install btop duf fastfetch fd-find fish fzf git gtypist luarocks neovim ripgrep vim
sudo dnf install francis haruna kate keepassxc kitty konversation ktorrent sqlitebrowser thunderbird
sudo dnf install clamav clamd clamav-update
sudo dnf install pandoc texlive-scheme-basic texlive-babel-portuges 'tex(moderncv.cls)' 'tex(academicons.sty)' 'tex(multirow.sty)' 'tex(arydshln.sty)' 'tex(fontawesome5.sty)' langpacks-pt_BR
```

### Brave Browser

Install Brave.

```
flatpak install flathub com.brave.Browser
```

### Pika Backup

Install Pika Backup.

```
flatpak install flathub org.gnome.World.PikaBackup
```

### Telegram

Install Telegram.

```
flatpak install flathub org.telegram.desktop
```

### Chezmoi

Install chezmoi.

```
sudo snap install chezmoi --classic
```

### Google Cloud CLI

Install Google Cloud CLI.

```
sudo snap install google-cloud-cli --classic
```

## Virtualization

Install Virtual Machine Manager.

```
sudo dnf install @virtualization
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
```

## Plymouth

Change the Plymouth theme to see systemd boot.

```
sudo plymouth-set-default-theme -R details
```

## Fish

Change the login shell to Fish.

```
sudo usermod --shell /usr/bin/fish $USER
```

## Iosevka

Install Iosevka Font.

```
mkdir -p ~/.local/share/fonts/Iosevka
cd ~/.local/share/fonts/Iosevka
curl -OL https://github.com/be5invis/Iosevka/releases/download/v32.3.1/SuperTTC-Iosevka-32.3.1.zip
unzip SuperTTC-Iosevka-32.3.1.zip
rm SuperTTC-Iosevka-32.3.1.zip
cd
fc-cache
```

## Neovim

Clone Neovim configuration.

```
git clone https://github.com/hmccl/nvim.git $HOME/.config/nvim
```

## KDE

KDE configuration.

- Caps Lock as Ctrl
- Create shortcuts
- Choose dark theme
- Remove animations
- Deactivate sleep

## Other

### Thuderbird

Configure Thunderbird to [use plain text email](https://useplaintext.email/#thunderbird).

### dotfiles

Clone dotfiles.

- `.boto`
- `.gitconfig`
- `.vimrc`
- `config.fish`
- `kitty.conf`

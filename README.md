# Fedora 40 KDE Plasma Setup

This is a guide to setup Fedora 40 KDE.

## First boot

Clean up the dnf cache and upgrade the system. Wait for 5 minutes (in case of a kernel update) and reboot.

```
sudo dnf clean all
sudo dnf upgrade
sudo dnf autoremove
```

After reboot make sure that the system is up to date.

## RPM Fusion

RPM Fusion is a repository that contains free and nonfree software.

### Multimedia

Install multimedia codecs.

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager --enable fedora-cisco-openh264
sudo dnf groupupdate core
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf groupupdate multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
```

### Intel and NVIDIA

Install Intel and NVIDIA drivers.

```
sudo dnf install intel-media-driver
sudo dnf install akmod-nvidia
```

Wait 5 minutes and reboot.

## Packages

Remove and install packages.

```
sudo dnf remove dragon kmahjongg kmines kpat skanpage akregator kaddressbook kde-connect krdc krfb kmail ktnef pim-data-exporter kontact korganizer kgpg kmousetool kmouth
sudo dnf install chicken duf fastfetch fd-find fish fzf git golang gtypist luarocks neovim ripgrep vim
sudo dnf install francis haruna kate keepassxc konversation ktorrent thunderbird
sudo dnf install sqlitebrower
sudo dnf install clamav clamd clamav-update
sudo dnf install texlive-scheme-basic texlive-babel-portuges pandoc 'tex(moderncv.cls)' 'tex(academicons.sty)' 'tex(multirow.sty)' 'tex(arydshln.sty)' 'tex(fontawesome5.sty)'
```

## Flathub

Enable the Flathub remote.

```
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Snap

Install snapd.

```
sudo dnf install snapd
sudo ln -s /var/lib/snapd/snap /snap
```

### Brave Browser

Install Brave.

```
sudo snap install brave-browser
```

### Google Cloud CLI

Install Google Cloud CLI.

```
sudo snap install google-cloud-cli --classic
```

Start gcloud.

```
gcloud init
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

Install Iosevka Nerd Font.

```
mkdir -p ~/.local/share/fonts/Iosevka
cd ~/.local/share/fonts/Iosevka
curl -OL https://github.com/ryanoasis/nerd-fonts/releases/latest/download/Iosevka.tar.xz
tar xvf Iosevka.tar.xz
rm Iosevka.tar.xz
cd
fc-cache -v
```

## Neovim

Clone Neovim configuration.

```
git clone https://github.com/hmccl/nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

## Minor tweaks

Configure Thunderbird to [use plain text email](https://useplaintext.email/#thunderbird).

Clone other configuration files like `.boto`, `.gitconfig` and `.vimrc`.

Remap Caps Lock to Ctrl.

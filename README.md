# Fedora 40 KDE Plasma Setup

## First boot

Clean up the dnf cache and upgrade the system. Wait for 5 minutes (in case of a kernel update) and reboot.

```
sudo dnf clean all
sudo dnf upgrade
sudo dnf autoremove
```

## RPM Fusion

### Multimedia

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf config-manager --enable fedora-cisco-openh264
sudo dnf groupupdate core
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf groupupdate multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
```

### Intel and Nvidia

```
sudo dnf install intel-media-driver
sudo dnf install akmod-nvidia
```

## Brave Browser

```
sudo dnf install dnf-plugins-core
sudo dnf config-manager --add-repo https://brave-browser-rpm-release.s3.brave.com/brave-browser.repo
sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc
sudo dnf install brave-browser
```

## Google Cloud CLI

```
sudo tee -a /etc/yum.repos.d/google-cloud-sdk.repo << EOM
[google-cloud-cli]
name=Google Cloud CLI
baseurl=https://packages.cloud.google.com/yum/repos/cloud-sdk-el9-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=0
gpgkey=https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOM
sudo dnf install google-cloud-cli
```

```
gcloud init
```

## Flathub

```
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Plymouth

```
sudo plymouth-set-default-theme -R details
```

## Programs

```
sudo dnf remove dragon kmahjongg kmines kpat skanpage akregator kaddressbook kde-connect krdc krfb kmail ktnef pim-data-exporter kontact korganizer kgpg kmousetool kmouth
sudo dnf install fd-find fzf git golang gtypist luarocks neovim ripgrep vim zsh
sudo dnf install francis haruna kate keepassxc konversation ktorrent thunderbird
sudo dnf install clamav clamd clamav-update
sudo dnf install texlive-scheme-basic texlive-babel-portuges pandoc 'tex(moderncv.cls)' 'tex(academicons.sty)' 'tex(multirow.sty)' 'tex(arydshln.sty)' 'tex(fontawesome5.sty)'
```

## ZSH

```
sudo usermod --shell /usr/bin/zsh helio
```

## Zim

```
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
```

## Iosevka

```
mkdir -p ~/.local/share/fonts/Iosevka
cd ~/.local/share/fonts/Iosevka
curl -OL https://github.com/ryanoasis/nerd-fonts/releases/latest/download/Iosevka.tar.xz
tar xvf Iosevka.tar.xz
rm Iosevka.tar.xz
cd
fc-cache -v
```

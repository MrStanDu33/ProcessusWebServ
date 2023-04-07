![GitHub last commit](https://img.shields.io/github/last-commit/mrstandu33/ProcessusWebServ/main)
![GitHub repo size](https://img.shields.io/github/repo-size/mrstandu33/ProcessusWebServ)
[![GitHub license](https://img.shields.io/github/license/mrstandu33/ProcessusWebServ.svg)](https://github.com/mrstandu33/ProcessusWebServ/blob/master/LICENSE)

[![time tracker](https://wakatime.com/badge/github/mrstandu33/ProcessusWebServ.svg)](https://wakatime.com/badge/github/mrstandu33/ProcessusWebServ)
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/cbb906d5cbe54eedbdf881f627bfbea6)](https://app.codacy.com/gh/MrStanDu33/ProcessusWebServ/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)
[![HitCount](https://img.shields.io/endpoint?url=https%3A%2F%2Fhits.dwyl.com%2FMrStanDu33%2FProcessusWebServ.json%3Fcolor%3DGREEN)](http://hits.dwyl.com/MrStanDu33/ProcessusWebServ)

[![Twitch Status](https://img.shields.io/twitch/status/mrstandu33)](https://twitch.tv/mrstandu33)

# Table of content

<details>
  <ul>
    <li><a href="#table-of-content">Table of content</a></li>
    <li>
      <a href="#setup-instructions">Setup instructions</a>
      <ul>
        <li><a href="#install-web-server">Install Web Server</a></li>
        <li><a href="#setup-windows-terminal">Setup Windows Terminal</a></li>
        <li>
          <a href="#setup-wsl2">Setup WSL2</a>
          <ul>
            <li>
              <a href="#basics">Basics</a>
              <ul>
                <li><a href="#setup-wsl-behavior">Setup WSL behavior</a></li>
                <li><a href="#setup-zsh">Setup ZSH</a></li>
                <li><a href="#setup-git-and-github">Setup GitHub and GitHub</a></li>
              </ul>
            </li>
            <li>
              <a href="#ease-of-use">Ease of use</a>
              <ul>
                <li><a href="#setup-bash-aliases">Setup bash aliases</a></li>
                <li><a href="#setup-terminal-colors">Setup terminal colors</a></li>
                <li><a href="#setup-wakatime-api">Setup Wakatime</a></li>
                <li><a href="#setup-powerline-theme">Setup Powerline theme</a></li>
                <li><a href="#setup-neofetch">Setup Neofetch</a></li>
              </ul>
            </li>
          </ul>
        </li>
        <li><a href="#install-phpmyadmin">Install phpMyAdmin</a></li>
        <li><a href="#install-node-version-manager-nvm">Install Node Version Manager (NVM)</a></li>
        <li><a href="#create-apache2-virtualhost">Create Apache2 VirtualHost</a></li>
        <li>
          <a href="#create-user">Create users</a>
          <ul>
            <li><a href="#mysql-user">MySQL users</a></li>
            <li><a href="#unix-user">Unix users</a></li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</details>

# Setup instructions

## Install Web Server

```bash
$ sudo su && \
$ apt-get clean -y && \
apt-get update -y && \
apt-get upgrade -y && \
apt-get full-upgrade -y && \
apt-get install -y curl wget lsb-release apt-transport-https ca-certificates apache2 apache2-doc apache2-utils curl mariadb-server sendmail python3-pip git unzip emacs php8.2 php8.2-{common,curl,bcmath,intl,mbstring,xmlrpc,mcrypt,mysql,gd,xml,cli,zip} man bat exa pipx && \
curl -sS https://getcomposer.org/installer -o composer-setup.php && \
php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
a2enmod rewrite && \
sendmailconfig && \
service apache2 restart && \
apt autoremove -y && \
mkdir -p ~/.local/bin && \
ln -s /usr/bin/batcat ~/.local/bin/bat
```

## Setup Windows Terminal

> https://www.microsoft.com/fr-fr/p/windows-terminal-preview/9n0dx20hk701

- Here is some basic configurations :

```json
{
  "$help": "https://aka.ms/terminal-documentation",
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "actions": [
    {
      "command": {
        "action": "copy",
        "singleLine": false
      },
      "keys": "ctrl+c"
    },
    {
      "command": "paste",
      "keys": "ctrl+v"
    },
    {
      "command": "find",
      "keys": "ctrl+shift+f"
    },
    {
      "command": {
        "action": "splitPane",
        "split": "auto",
        "splitMode": "duplicate"
      },
      "keys": "alt+shift+d"
    }
  ],
  "copyFormatting": "none",
  "copyOnSelect": false,
  "defaultProfile": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
  "newTabMenu": [
    {
      "type": "remainingProfiles"
    }
  ],
  "profiles": {
    "defaults": {
      "elevate": true,
      "font": {
        "face": "CaskaydiaCove Nerd Font Mono"
      }
    },
    "list": [
      {
        "commandline": "%SystemRoot%\\System32\\cmd.exe",
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "hidden": false,
        "name": "Invite de commandes"
      },
      {
        "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "hidden": false,
        "name": "Windows PowerShell"
      },
      {
        "guid": "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
        "hidden": false,
        "name": "Debian",
        "opacity": 72,
        "source": "Windows.Terminal.Wsl",
        "useAcrylic": true
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": false,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ]
  },
  "schemes": [
    {
      "background": "#0C0C0C",
      "black": "#0C0C0C",
      "blue": "#0037DA",
      "brightBlack": "#767676",
      "brightBlue": "#3B78FF",
      "brightCyan": "#61D6D6",
      "brightGreen": "#16C60C",
      "brightPurple": "#B4009E",
      "brightRed": "#E74856",
      "brightWhite": "#F2F2F2",
      "brightYellow": "#F9F1A5",
      "cursorColor": "#FFFFFF",
      "cyan": "#3A96DD",
      "foreground": "#CCCCCC",
      "green": "#13A10E",
      "name": "Campbell",
      "purple": "#881798",
      "red": "#C50F1F",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#C19C00"
    },
    {
      "background": "#012456",
      "black": "#0C0C0C",
      "blue": "#0037DA",
      "brightBlack": "#767676",
      "brightBlue": "#3B78FF",
      "brightCyan": "#61D6D6",
      "brightGreen": "#16C60C",
      "brightPurple": "#B4009E",
      "brightRed": "#E74856",
      "brightWhite": "#F2F2F2",
      "brightYellow": "#F9F1A5",
      "cursorColor": "#FFFFFF",
      "cyan": "#3A96DD",
      "foreground": "#CCCCCC",
      "green": "#13A10E",
      "name": "Campbell Powershell",
      "purple": "#881798",
      "red": "#C50F1F",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#C19C00"
    },
    {
      "background": "#282C34",
      "black": "#282C34",
      "blue": "#61AFEF",
      "brightBlack": "#5A6374",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B6C2",
      "brightGreen": "#98C379",
      "brightPurple": "#C678DD",
      "brightRed": "#E06C75",
      "brightWhite": "#DCDFE4",
      "brightYellow": "#E5C07B",
      "cursorColor": "#FFFFFF",
      "cyan": "#56B6C2",
      "foreground": "#DCDFE4",
      "green": "#98C379",
      "name": "One Half Dark",
      "purple": "#C678DD",
      "red": "#E06C75",
      "selectionBackground": "#FFFFFF",
      "white": "#DCDFE4",
      "yellow": "#E5C07B"
    },
    {
      "background": "#FAFAFA",
      "black": "#383A42",
      "blue": "#0184BC",
      "brightBlack": "#4F525D",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B5C1",
      "brightGreen": "#98C379",
      "brightPurple": "#C577DD",
      "brightRed": "#DF6C75",
      "brightWhite": "#FFFFFF",
      "brightYellow": "#E4C07A",
      "cursorColor": "#4F525D",
      "cyan": "#0997B3",
      "foreground": "#383A42",
      "green": "#50A14F",
      "name": "One Half Light",
      "purple": "#A626A4",
      "red": "#E45649",
      "selectionBackground": "#FFFFFF",
      "white": "#FAFAFA",
      "yellow": "#C18301"
    },
    {
      "background": "#002B36",
      "black": "#002B36",
      "blue": "#268BD2",
      "brightBlack": "#073642",
      "brightBlue": "#839496",
      "brightCyan": "#93A1A1",
      "brightGreen": "#586E75",
      "brightPurple": "#6C71C4",
      "brightRed": "#CB4B16",
      "brightWhite": "#FDF6E3",
      "brightYellow": "#657B83",
      "cursorColor": "#FFFFFF",
      "cyan": "#2AA198",
      "foreground": "#839496",
      "green": "#859900",
      "name": "Solarized Dark",
      "purple": "#D33682",
      "red": "#DC322F",
      "selectionBackground": "#FFFFFF",
      "white": "#EEE8D5",
      "yellow": "#B58900"
    },
    {
      "background": "#FDF6E3",
      "black": "#002B36",
      "blue": "#268BD2",
      "brightBlack": "#073642",
      "brightBlue": "#839496",
      "brightCyan": "#93A1A1",
      "brightGreen": "#586E75",
      "brightPurple": "#6C71C4",
      "brightRed": "#CB4B16",
      "brightWhite": "#FDF6E3",
      "brightYellow": "#657B83",
      "cursorColor": "#002B36",
      "cyan": "#2AA198",
      "foreground": "#657B83",
      "green": "#859900",
      "name": "Solarized Light",
      "purple": "#D33682",
      "red": "#DC322F",
      "selectionBackground": "#FFFFFF",
      "white": "#EEE8D5",
      "yellow": "#B58900"
    },
    {
      "background": "#000000",
      "black": "#000000",
      "blue": "#3465A4",
      "brightBlack": "#555753",
      "brightBlue": "#729FCF",
      "brightCyan": "#34E2E2",
      "brightGreen": "#8AE234",
      "brightPurple": "#AD7FA8",
      "brightRed": "#EF2929",
      "brightWhite": "#EEEEEC",
      "brightYellow": "#FCE94F",
      "cursorColor": "#FFFFFF",
      "cyan": "#06989A",
      "foreground": "#D3D7CF",
      "green": "#4E9A06",
      "name": "Tango Dark",
      "purple": "#75507B",
      "red": "#CC0000",
      "selectionBackground": "#FFFFFF",
      "white": "#D3D7CF",
      "yellow": "#C4A000"
    },
    {
      "background": "#FFFFFF",
      "black": "#000000",
      "blue": "#3465A4",
      "brightBlack": "#555753",
      "brightBlue": "#729FCF",
      "brightCyan": "#34E2E2",
      "brightGreen": "#8AE234",
      "brightPurple": "#AD7FA8",
      "brightRed": "#EF2929",
      "brightWhite": "#EEEEEC",
      "brightYellow": "#FCE94F",
      "cursorColor": "#000000",
      "cyan": "#06989A",
      "foreground": "#555753",
      "green": "#4E9A06",
      "name": "Tango Light",
      "purple": "#75507B",
      "red": "#CC0000",
      "selectionBackground": "#FFFFFF",
      "white": "#D3D7CF",
      "yellow": "#C4A000"
    },
    {
      "background": "#300A24",
      "black": "#171421",
      "blue": "#0037DA",
      "brightBlack": "#767676",
      "brightBlue": "#08458F",
      "brightCyan": "#2C9FB3",
      "brightGreen": "#26A269",
      "brightPurple": "#A347BA",
      "brightRed": "#C01C28",
      "brightWhite": "#F2F2F2",
      "brightYellow": "#A2734C",
      "cursorColor": "#FFFFFF",
      "cyan": "#3A96DD",
      "foreground": "#FFFFFF",
      "green": "#26A269",
      "name": "Ubuntu-22.04-ColorScheme",
      "purple": "#881798",
      "red": "#C21A23",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#A2734C"
    },
    {
      "background": "#000000",
      "black": "#000000",
      "blue": "#000080",
      "brightBlack": "#808080",
      "brightBlue": "#0000FF",
      "brightCyan": "#00FFFF",
      "brightGreen": "#00FF00",
      "brightPurple": "#FF00FF",
      "brightRed": "#FF0000",
      "brightWhite": "#FFFFFF",
      "brightYellow": "#FFFF00",
      "cursorColor": "#FFFFFF",
      "cyan": "#008080",
      "foreground": "#C0C0C0",
      "green": "#008000",
      "name": "Vintage",
      "purple": "#800080",
      "red": "#800000",
      "selectionBackground": "#FFFFFF",
      "white": "#C0C0C0",
      "yellow": "#808000"
    }
  ],
  "themes": [],
  "useAcrylicInTabRow": true
}
```

## Setup WSL2

### Basics

#### Setup WSL behavior

1. Type in your terminal :

```bash
$ emacs /etc/wsl.conf
```

1. Write inside the file :

```conf
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"
[Interop]
appendWindowsPath = true
[boot]
systemd=true
[user]
default=root
```

3. Type in Command Prompt :

```bash
> wsl -l
# get wsl name
> wsl -t $NANE
> $NAME config --default-user root
```

---

#### Setup ZSH

1. Type in your terminal :

```bash
$ apt-get install -y zsh
$ chsh
$ /bin/zsh
$ cd ~
$ curl -L git.io/antigen > antigen.zsh
$ emacs ~/.zshrc
```

2. Write inside the file :

```bash
source ~/antigen.zsh

antigen use oh-my-zsh

antigen bundle git
antigen bundle pip
antigen bundle github
antigen bundle npm
antigen bundle command-not-found
#antigen bundle common-aliases # Warning : enabling this line breaks NVM.
antigen bundle compleat
antigen bundle git-extras

antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle zsh-users/zsh-completions
antigen bundle zsh-users/zsh-autosuggestions

antigen bundle bobsoppe/zsh-ssh-agent

antigen apply
```

---

#### Setup Git and GitHub

> https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key

1. Type in your terminal :

```bash
$ apt-get install -y keychain
$ ssh-keygen -t ed25519 -C "email@example.com"
$ git config --global user.name "John Doe"
$ git config --global user.email "email@example.com"
$ git config --global gpg.format ssh
$ git config --global commit.gpgsign true
$ git config --global tag.gpgsign true
$ cat ~/.ssh/id_ed25519.pub
$ git config --global user.signingKey 'ssh-ed25519 AAAAC3(...)qiXsb email@example.com' # with key seen from previous command
$ emacs ~/.config/git/allowed_signers
```

2. Then write in file :

```conf
email@example.com ssh-ed25519 AAAAC3(...)qiXsb email@example.com
```

3. Type in your terminal :

```bash
$ emacs ~/.gitconfig
```

4. Add in this file :

```bash
[gpg "ssh"]
        allowedSignersFile = /path/to/your_user/.ssh/allowed_signers
[core]
        fileMode = false
        editor = emacs
[pull]
        rebase = false
[init]
        defaultBranch = main
```

5. Then, go to your [SSH and GPG key settings page](https://github.com/settings/keys), and add your SSH key to your account as a signing key and as an authentication key.

6. Add to your Visual Studio Code JSON settings file this line:

```json
"git.enableCommitSigning": true
```

7. Type in your terminal :

```bash
$ emacs ~/.zshrc
```

8. Finally, add in the file :

```bash
##### Start SSH agent autoload #####
  /usr/bin/keychain --nogui $HOME/.ssh/id_ed25519
  source $HOME/.keychain/$HOST-sh
##### End SSH agent autoload #####
```

---

### Ease of use

#### Setup bash aliases

1. Type in your terminal :

```bash
$ emacs ~/.zshrc
```

2. Write inside the file :

```bash
##### Start Aliases setup #####
  alias ssh="ssh -A" # Enable connection transfer of authentication agent.
  alias emacs="emacs -nw" # Force emacs to open as non window mode.
  alias cat='bat' # Replaces /usr/bin/cat with bat.
  alias ls='exa' # Replaces /usr/bin/ls with exa.
  alias ll='exa -la --icons' # Enable exa command with icons.
##### End Aliases setup #####
```

---

#### Setup terminal colors

1. Type in your terminal :

```bash
$ emacs ~/.zshrc
```

2. Write inside the file :

```bash
##### Start Terminal Color enabling #####
  eval "`dircolors`" # Enable colors for ls.
  force_color_prompt=yes # Enable color for terminal.
##### End Terminal Color enabling #####
```

---

#### Setup Wakatime

> https://wakatime.com/terminal#install-bash

1. First, type in your terminal :

```bash
  $ pipx install wakatime
  $ pipx ensurepath
  $ emacs ~/.zshrc
```

2. Write inside the file before `antigen apply` :

```bash
  antigen bundle sobolevn/wakatime-zsh-plugin
```

3. Visit https://wakatime.com/settings/account and copy your API KEY
4. Type in your terminal :

```bash
$ emacs ~/.wakatime.cfg
```

5. Write inside the file :

```conf
[settings]
api_key = YOUR_API_KEY
```

---

#### Setup Powerline theme

> https://github.com/justjanne/powerline-go

1. First, type in your terminal :

```bash
$ pipx install powerline-status
$ emacs ~/.zshrc
```

2. Write inside the file before `antigen apply` :

```bash
antigen bundle Lokaltog/powerline powerline/bindings/zsh
```

3. Visit https://github.com/ryanoasis/nerd-fonts/releases, download `CascadiaCode.zip` and install it on Windows.

---

#### Setup neofetch

> https://github.com/dylanaraps/neofetch

1. Type in your terminal :

```bash
$ apt-get install neofetch
$ emacs ~/.zshrc
```

2. Write inside the file :

```bash
##### Start Neofetch enabling #####
  neofetch # Runs neofetch at startup.
##### End Neofetch enabling #####
```

4. Type in your terminal :

```bash
$ emacs ~/.config/neofetch/config
```

5. Write inside the file :

```bash
# Source: https://github.com/Chick2D/neofetch-themes/
# Made by https://github.com/MrStanDu33
# Customization Wiki https://github.com/dylanaraps/neofetch/wiki/Customizing-Info

print_info() {
    prin
    prin
    prin "$(color 13)╭─ $(color 10)Software$(color 13) ──────────────────────────────────────────╮"
    prin "$(color 13)│                                                     │"
    info "$(color 13)  $(color 14)OS" distro
    info "$(color 13)  $(color 14)Kernel" kernel
    info "$(color 13)  $(color 14)Packages" packages
    info "$(color 13)  $(color 14)Shell" shell
    info "$(color 13)  $(color 14)Terminal" term
    info "$(color 13)  $(color 14)Local IP"local_ip
    info "$(color 13)  $(color 14)Wan IP" public_ip
    prin "$(color 13)│                                                     │"
    prin "$(color 13)├─ $(color 10)Hardware$(color 13) ──────────────────────────────────────────┤"
    prin "$(color 13)│                                                     │"
    info "$(color 13)  $(color 14)CPU" cpu
    info "$(color 13)  $(color 14)GPU" gpu
    info "$(color 13)  $(color 14)Memory" memory
    info "$(color 13)  $(color 14)Disk" disk
    prin "$(color 13)│                                                     │"
    prin "$(color 13)├─ $(color 10)Session$(color 13) ───────────────────────────────────────────┤"
    prin "$(color 13)│                                                     │"
    info "$(color 13)  $(color 14)User" title
    info "$(color 13)  $(color 14)Uptime" uptime
    prin "$(color 13)│                                                     │"
    prin "$(color 13)╰─────────────────────────────────────────────────────╯"
    info cols
}

# To know what these functions mean, go to the Customization Wiki on top

# Title
title_fqdn="on"

# Kernel
kernel_shorthand="off"

# Distro
distro_shorthand="off"
os_arch="off"

# Uptime
uptime_shorthand="off"

# Memory
memory_percent="on"
memory_unit="gib"

# Packages
package_managers="on"

# Shell
shell_path="on"
shell_version="on"

# CPU
speed_type="bios_limit"
speed_shorthand="on"
cpu_brand="on"
cpu_speed="on"
cpu_cores="logical"
cpu_temp="off"

# GPU
gpu_brand="on"
gpu_type="all"

# Resolution
refresh_rate="on"

# Gtk Theme / Icons / Font
gtk_shorthand="on"
gtk2="on"
gtk3="on"

# IP Address
public_ip_host="http://ident.me"
public_ip_timeout=2

# Desktop Environment
de_version="on"

# Disk
disk_show=('/' '/mnt/c')
disk_subtitle="dir"
disk_percent="on"

# Song
music_player="spotify"
song_format="%artist% - %album% - %title%"
song_shorthand="on"
mpc_args=()

# Text Colors
colors=(distro)

# Text Options
bold="on"
underline_enabled="on"
underline_char="-"
separator="›"

# Color Blocks
block_range=(0 15)
color_blocks="on"
block_width=3
block_height=1
col_offset="auto"

# Progress Bars
bar_char_elapsed="▰"
bar_char_total="▱"
bar_border="on"
bar_length=20
bar_color_elapsed="distro"
bar_color_total="distro"

# Info display
cpu_display="infobar"
memory_display="infobar"
battery_display="infobar"
disk_display="infobar"

# Backend Settings
image_backend="ascii"
image_source="auto"

# Ascii Options
ascii_distro="auto"
ascii_colors=(distro)
ascii_bold="on"

# Image Options
image_loop="off"
thumbnail_dir="${XDG_CACHE_HOME:-${HOME}/.cache}/thumbnails/neofetch"
crop_mode="fit"
crop_offset="center"
image_size="auto"
gap=-420
yoffset=0
xoffset=0
background_color=

# Misc Options
stdout="off"
```

<br/>

## Install phpMyAdmin

1. Type in your terminal :

```bash
$ cd /var/www/
$ wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.zip
$ unzip phpMyAdmin-latest-all-languages.zip
$ rm -f phpMyAdmin-latest-all-languages.zip
$ mv phpMyAdmin-* phpmyadmin.localhost/
$ cd phpmyadmin.localhost
$ mkdir ./tmp
$ chown -R www-data:www-data ./tmp
$ chmod -R 755 ./tmp
$ cp ./config.sample.inc.php ./config.inc.php
$ emacs ./config.inc.php
```

2. Then, go to [this url](https://phpsolved.com/phpmyadmin-blowfish-secret-generator/) and copy the code inside the second code block.
3. Then, replace this line with what you copied:

```php
$cfg['blowfish_secret'] = '';
```

4. And add this line to the config file :

```php
$cfg['TempDir'] = 'tmp';
```

5. Finally, create an Apache Virtual Host as described [here](#create-apache2-virtualhost)

## Install Node Version Manager (NVM)

> https://github.com/nvm-sh/nvm

1. Type in your terminal :

```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
$ emacs ~/.zshrc
```

2. Then check if, at the end of the file, you have these lines (if not, add them.):

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

## Create Apache2 VirtualHost

> Here, `sub.domain.tld` is meant to be replaced with your domain name.

1. Type in your terminal :

```bash
$ emacs /etc/apache2/sites-available/sub.domain.tld.conf
```

2. Write inside the file :n

```conf
<VirtualHost *:80>
  ServerName sub.domain.tld
  ServerAlias sub2.domain.tld # only if necessary
  DocumentRoot /var/www/sub.domain.tld/

  ErrorLog /var/log/apache2/sub.domain.tld.error.log
  CustomLog /var/log/apache2/sub.domain.tld.access.log combined
</VirtualHost>
```

3. Type in your terminal :

```bash
$ a2ensite sub.domain.tld
$ service apache2 restart
```

<br/>

## Create users

### MySQL users

1. Type in your terminal :

```bash
$ mysql -u root -p
```

2. Type in SQL prompt :

```SQL
> CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
> CREATE DATABASE database;
> GRANT ALL PRIVILEGES ON database.* TO 'user'@'localhost';
> FLUSH PRIVILEGES;
> exit;
```

### Unix users

1. Type in your terminal :

```bash
$ NEWUSER=nomprenom
$ useradd -m -s /bin/bash $NEWUSER
$ chmod 755 /home/$NEWUSER
$ rm /home/$NEWUSER/.bashrc
$ usermod -g www-data $NEWUSER
$ emacs /home/$NEWUSER/.bash_profile
```

1. Write inside the file :

```bash
alias ls='ls --color=auto'
##### Start Alias access blocking #####
alias su="printf ''"
alias sudo="printf ''"
alias apt-get="printf ''"
alias aptitude="printf ''"
alias exit="printf ''"
alias logout="printf ''"
alias passwd="printf ''"
alias rlogin="printf ''"
alias ssh="printf ''"
alias slogin="printf ''"
alias yppasswd="printf ''"
alias mail="printf ''"
alias mesg="printf ''"
alias pine="printf ''"
alias talk="printf ''"
alias write="printf ''"
alias as="printf ''"
alias awk="printf ''"
alias bc="printf ''"
alias cc="printf ''"
alias csh="printf ''"
alias dbx="printf ''"
alias f77="printf ''"
alias gdb="printf ''"
alias gprof="printf ''"
alias kill="printf ''"
alias ld="printf ''"
alias lex="printf ''"
alias lint="printf ''"
alias make="printf ''"
alias maple="printf ''"
alias math="printf ''"
alias nice="printf ''"
alias nohup="printf ''"
alias pc="printf ''"
alias perl="printf ''"
alias prof="printf ''"
alias python="printf ''"
alias sh="printf ''"
alias yacc="printf ''"
alias xcalc="printf ''"
alias apropos="printf ''"
alias find="printf ''"
alias info="printf ''"
alias man="printf ''"
alias whatis="printf ''"
alias whereis="printf ''"
alias chmod="printf ''"
alias chown="printf ''"
alias chgrp="printf ''"
alias cmp="printf ''"
alias comm="printf ''"
alias cp="printf ''"
alias crypt="printf ''"
alias diff="printf ''"
alias file="printf ''"
alias grep="printf ''"
alias gzip="printf ''"
alias ln="printf ''"
alias lsof="printf ''"
alias mkdir="printf ''"
alias mv="printf ''"
alias pwd="printf ''"
alias quota="printf ''"
alias rm="printf ''"
alias rmdir="printf ''"
alias stat="printf ''"
alias sync="printf ''"
alias sort="printf ''"
alias tar="printf ''"
alias tee="printf ''"
alias tr="printf ''"
alias umask="printf ''"
alias uncompress="printf ''"
alias uniq="printf ''"
alias cat="printf ''"
alias fold="printf ''"
alias head="printf ''"
alias lpq="printf ''"
alias lpr="printf ''"
alias lprm="printf ''"
alias more="printf ''"
alias less="printf ''"
alias page="printf ''"
alias pr="printf ''"
alias tail="printf ''"
alias zcat="printf ''"
alias xv="printf ''"
alias gv="printf ''"
alias xpdf="printf ''"
alias ftp="printf ''"
alias rsync="printf ''"
alias scp="printf ''"
alias alias="printf ''"
alias chquota="printf ''"
alias chsh="printf ''"
alias clear="printf ''"
alias echo="printf ''"
alias pbm="printf ''"
alias popd="printf ''"
alias pushd="printf ''"
alias script="printf ''"
alias setenv="printf ''"
alias stty="printf ''"
alias netstat="printf ''"
alias rsh="printf ''"
alias ssh="printf ''"
alias bg="printf ''"
alias fg="printf ''"
alias jobs="printf ''"
alias ^y="printf ''"
alias ^z="printf ''"
alias clock="printf ''"
alias date="printf ''"
alias df="printf ''"
alias du="printf ''"
alias env="printf ''"
alias finger="printf ''"
alias history="printf ''"
alias last="printf ''"
alias lpq="printf ''"
alias manpath="printf ''"
alias printenv="printf ''"
alias ps="printf ''"
alias pwd="printf ''"
alias set="printf ''"
alias spend="printf ''"
alias stty="printf ''"
alias time="printf ''"
alias top="printf ''"
alias uptime="printf ''"
alias w="printf ''"
alias who="printf ''"
alias whois="printf ''"
alias whoami="printf ''"
alias gimp="printf ''"
alias xfig="printf ''"
alias xv="printf ''"
alias xvscan="printf ''"
alias xpaint="printf ''"
alias kpaint="printf ''"
alias mplayer="printf ''"
alias realplay="printf ''"
alias timidity="printf ''"
alias xmms="printf ''"
alias abiword="printf ''"
alias addbib="printf ''"
alias col="printf ''"
alias diction="printf ''"
alias diffmk="printf ''"
alias dvips="printf ''"
alias explain="printf ''"
alias grap="printf ''"
alias hyphen="printf ''"
alias ispell="printf ''"
alias latex="printf ''"
alias pdfelatex="printf ''"
alias latex2html="printf ''"
alias lookbib="printf ''"
alias macref="printf ''"
alias ndx="printf ''"
alias neqn="printf ''"
alias nroff="printf ''"
alias pic="printf ''"
alias psdit="printf ''"
alias ptx="printf ''"
alias refer="printf ''"
alias roffbib="printf ''"
alias sortbib="printf ''"
alias spell="printf ''"
alias ispell="printf ''"
alias style="printf ''"
alias tbl="printf ''"
alias tex="printf ''"
alias tpic="printf ''"
alias wget="printf ''"
alias grabmode="printf ''"
alias import="printf ''"
alias xdpyinfo="printf ''"
alias xkill="printf ''"
alias xlock="printf ''"
alias xterm="printf ''"
alias xwininfo="printf ''"
alias html2ps="printf ''"
alias latex2html="printf ''"
alias lynx="printf ''"
alias netscape="printf ''"
alias sitecopy="printf ''"
alias weblint="printf ''"
alias vi="vi -Z" #this is vi's safe mode and shell commands won't be run from within vi
alias alias="printf ''"
##### End Alias access blocking #####
```

3. Type in your terminal :

```bash
$ chown root:root /home/$NEWUSER/.bash_profile
$ chmod 755 /home/$NEWUSER/.bash_profile
$ ssh-keygen
```

- If user uses Windows system, or will use FileZilla (or any program that use .ppk key files) :
  <ul>
    <li>Download /home/$NEWUSER/.ssh/id_rsa</li>
    <li>Download PuTTY</li>
    <li>Install PuTTYgen and open it</li>
    <li>Click on `Conversions` > `Import key`</li>
    <li>Type passphrase</li>
    <li>Export private key to .ppk format</li>
  </ul>

4. Type in your terminal :

```bash
$ cat /home/$NEWUSER/.ssh/id_rsa.pub >> /home/$NEWUSER/.ssh/authorized_keys
$ chmod -R go= /home/$NEWUSER/.ssh/
$ chown -R $NEWUSER:$NEWUSER /home/$NEWUSER/.ssh/
```

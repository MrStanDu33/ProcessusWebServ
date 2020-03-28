# Table of content
- [Table of content](#table-of-content)
- [Setup instructions](#setup-instructions)
  - [Install Web Server](#install-web-server)
  - [Setup Windows Terminal](#setup-windows-terminal)
  - [Setup WSL2](#setup-wsl2)
    - [Basics](#basics)
      - [Setup WSL behavior](#setup-wsl-behavior)
      - [Setup GitHub SSH Key](#setup-github-ssh-key)
      - [Setup GitHub GPG Key](#setup-github-gpg-key)
      - [Setup Pinentry for WSL](#setup-pinentry-for-wsl)
    - [Ease of use](#ease-of-use)
      - [Setup bash aliases](#setup-bash-aliases)
      - [Setup terminal colors](#setup-terminal-colors)
      - [Setup autoclear RamCache](#setup-autoclear-ramcache)
      - [Setup autoload for Apache2](#setup-autoload-for-apache2)
      - [Setup autoload for MySQL](#setup-autoload-for-mysql)
      - [Setup Wakatime API](#setup-wakatime-api)
      - [Setup Powerline Go](#setup-powerline-go)
      - [Setup Archey4](#setup-archey4)
  - [Create Apache2 VirtualHost](#create-apache2-virtualhost)
  - [Create user](#create-user)
    - [MySQL user](#mysql-user)
    - [Unix user](#unix-user)

# Setup instructions

## Install Web Server

```bash
  $ apt-get update -y && \
  apt-get upgrade -y && \
  apt-get dist-upgrade -y && \
  apt-get install -y wget lsb-release apt-transport-https ca-certificates && \
  wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
  echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php7.4.list && \
  apt-get update -y && \
  apt-get install -y apache2 apache2-doc apache2-utils curl mariadb-server sendmail python3-pip git unzip emacs php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-pdo php7.4-mysql php7.4-zip php7.4-gd  php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath php7.4-json libapache2-mod-php7.4 php-cli php-mbstring nodejs npm && \
  curl -sS https://getcomposer.org/installer -o composer-setup.php && \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  a2enmod rewrite && \
  sendmailconfig && \
  service apache2 restart
```

## Setup Windows Terminal
> https://www.microsoft.com/fr-fr/p/windows-terminal-preview/9n0dx20hk701
* Here is some basic configurations :
  ```json
  {
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "globals" :
    {
      "alwaysShowTabs" : true,
      "defaultProfile" : "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
      "initialCols" : 120,
      "initialRows" : 30,
      "requestedTheme" : "system",
      "showTabsInTitlebar" : true,
      "showTerminalTitleInTitlebar" : true,
      "wordDelimiters" : " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502"
    },
    "profiles" :
    [
      {
        "acrylicOpacity" : 0.60,
        "background" : "#111111",
        "backgroundImageOpacity" : 0.60,
        "backgroundImageStretchMode" : "uniformToFill",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "wsl.exe -d Debian",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Delugia Nerd Font",
        "fontSize" : 11,
        "guid" : "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
        "historySize" : 9001,
        "name" : "Debian",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "startingDirectory" : "%USERPROFILE%",
        "tabTitle" : "Debian",
        "useAcrylic" : true
      },
      {
        "acrylicOpacity" : 0.60,
        "background" : "#111111",
        "backgroundImageOpacity" : 0.60,
        "backgroundImageStretchMode" : "uniformToFill",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "cmd.exe",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Delugia Nerd Font",
        "fontSize" : 11,
        "guid" : "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "historySize" : 9001,
        "name" : "Command Prompt",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "startingDirectory" : "%USERPROFILE%",
        "tabTitle" : "Command Prompt",
        "useAcrylic" : true
      },
      {
        "acrylicOpacity" : 0.75,
        "background" : "#012456",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "powershell.exe",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Delugia Nerd Font",
        "fontSize" : 11,
        "guid" : "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "historySize" : 9001,
        "name" : "Windows PowerShell",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "startingDirectory" : "%USERPROFILE%",
        "tabTitle" : "Command Prompt",
        "useAcrylic" : true
      },
      {
          "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
          "hidden": false,
          "name": "Azure Cloud Shell",
          "source": "Windows.Terminal.Azure"
      }
    ],
    "schemes" :
    [
      {
        "background" : "#0C0C0C",
        "black" : "#0C0C0C",
        "blue" : "#0037DA",
        "brightBlack" : "#767676",
        "brightBlue" : "#3B78FF",
        "brightCyan" : "#61D6D6",
        "brightGreen" : "#16C60C",
        "brightPurple" : "#B4009E",
        "brightRed" : "#E74856",
        "brightWhite" : "#F2F2F2",
        "brightYellow" : "#F9F1A5",
        "cyan" : "#3A96DD",
        "foreground" : "#CCCCCC",
        "green" : "#13A10E",
        "name" : "Campbell",
        "purple" : "#881798",
        "red" : "#C50F1F",
        "white" : "#CCCCCC",
        "yellow" : "#C19C00"
      },
      {
        "background" : "#282C34",
        "black" : "#282C34",
        "blue" : "#61AFEF",
        "brightBlack" : "#5A6374",
        "brightBlue" : "#61AFEF",
        "brightCyan" : "#56B6C2",
        "brightGreen" : "#98C379",
        "brightPurple" : "#C678DD",
        "brightRed" : "#E06C75",
        "brightWhite" : "#DCDFE4",
        "brightYellow" : "#E5C07B",
        "cyan" : "#56B6C2",
        "foreground" : "#DCDFE4",
        "green" : "#98C379",
        "name" : "One Half Dark",
        "purple" : "#C678DD",
        "red" : "#E06C75",
        "white" : "#DCDFE4",
        "yellow" : "#E5C07B"
      },
      {
        "background" : "#FAFAFA",
        "black" : "#383A42",
        "blue" : "#0184BC",
        "brightBlack" : "#4F525D",
        "brightBlue" : "#61AFEF",
        "brightCyan" : "#56B5C1",
        "brightGreen" : "#98C379",
        "brightPurple" : "#C577DD",
        "brightRed" : "#DF6C75",
        "brightWhite" : "#FFFFFF",
        "brightYellow" : "#E4C07A",
        "cyan" : "#0997B3",
        "foreground" : "#383A42",
        "green" : "#50A14F",
        "name" : "One Half Light",
        "purple" : "#A626A4",
        "red" : "#E45649",
        "white" : "#FAFAFA",
        "yellow" : "#C18301"
      },
      {
        "background" : "#002B36",
        "black" : "#073642",
        "blue" : "#268BD2",
        "brightBlack" : "#002B36",
        "brightBlue" : "#839496",
        "brightCyan" : "#93A1A1",
        "brightGreen" : "#586E75",
        "brightPurple" : "#6C71C4",
        "brightRed" : "#CB4B16",
        "brightWhite" : "#FDF6E3",
        "brightYellow" : "#657B83",
        "cyan" : "#2AA198",
        "foreground" : "#839496",
        "green" : "#859900",
        "name" : "Solarized Dark",
        "purple" : "#D33682",
        "red" : "#DC322F",
        "white" : "#EEE8D5",
        "yellow" : "#B58900"
      },
      {
        "background" : "#FDF6E3",
        "black" : "#073642",
        "blue" : "#268BD2",
        "brightBlack" : "#002B36",
        "brightBlue" : "#839496",
        "brightCyan" : "#93A1A1",
        "brightGreen" : "#586E75",
        "brightPurple" : "#6C71C4",
        "brightRed" : "#CB4B16",
        "brightWhite" : "#FDF6E3",
        "brightYellow" : "#657B83",
        "cyan" : "#2AA198",
        "foreground" : "#657B83",
        "green" : "#859900",
        "name" : "Solarized Light",
        "purple" : "#D33682",
        "red" : "#DC322F",
        "white" : "#EEE8D5",
        "yellow" : "#B58900"
      }
    ]
  }

  ```


## Setup WSL2

### Basics

#### Setup WSL behavior
* First :
  ```bash
  $ emacs /etc/wsl.conf
  ```
* Write inside :
  ```conf
  [automount]
  enabled = true
  options = "metadata,umask=22,fmask=11"
  [Interop]
  appendWindowsPath = False
  ```
* Then, in CMD :
  ```bash
  > wsl -l
  # get wsl name
  > wsl -t $NANE
  > $NAME config --default-user root
  ```
---
#### Setup GitHub SSH Key
> https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh
* First :
  ```bash
  $ ssh-keygen -t rsa -b 4096 -C "email@example.com"
  $ eval $(ssh-agent -s)
  $ ssh-add ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub
  # print on GitHub
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Auto start ssh-agent #####
  eval $(ssh-agent) > /dev/null 2>&1
  ##### End Auto start ssh-agent #####
  ```
---
#### Setup GitHub GPG Key
> https://help.github.com/en/github/authenticating-to-github/managing-commit-signature-verification
* First :
  ```bash
  $ gpg --full-generate-key
  $ gpg --list-secret-keys --keyid-format LONG
  $ gpg --armor --export $KEY # print on GitHub
  $ git config --global user.signingkey $KEY
  $ git config --global user.name "John Doe"
  $ git config --global user.email "email@example.com"
  # Set in VSCode settings.json -> "git.enableCommitSigning": true,
  ```
---
#### Setup Pinentry for WSL
> https://github.com/diablodale/pinentry-wsl-ps1
* First :
  ```bash
  $ cd /home/$USER/
  $ git clone https://github.com/diablodale/pinentry-wsl-ps1
  $ chmod ug=rx pinentry-wsl-ps1.sh
  $ emacs /root/.gnupg/gpg-agent.conf
  ```
* Write inside :
  ```conf
  enable-ssh-support
  disable-scdaemon
  pinentry-program /home/$USER/pinentry-wsl-ps1/pinentry-wsl-ps1.sh
  debug 1024
  debug-pinentry
  log-file /root/agent.log
  ```
* Then :
  ```bash
  $ gpg-connect-agent killagent /bye
  $ gpg-connect-agent /bye
  ```
* Finally :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Pinentry-WSL-PS1 enabling #####
  export GPGKEY=3922899C9BCA4AE4 # set prefered gpg signing key
  PIDFOUND=$(pgrep gpg-agent)
  if [ -n "$PIDFOUND" ]; then
    export GPG_AGENT_INFO="/root/.gnupg/S.gpg-agent:$PIDFOUND:1"
    export GPG_TTY=$(tty)
    export SSH_AUTH_SOCK="/root/.gnupg/S.gpg-agent.ssh"
    unset SSH_AGENT_PID
  fi
  PIDFOUND=$(pgrep dirmngr)
  if [ -n "$PIDFOUND" ]; then
    export DIRMNGR_INFO="/root/.gnupg/S.dirmngr:$PIDFOUND:1"
  fi
  unset PIDFOUND
  ##### End Pinentry-WSL-PS1 enabling #####
  ```
<br/>

### Ease of use

#### Setup bash aliases
* First :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Aliases setup #####
  alias ssh="ssh -A"
  alias emacs="emacs -nw"
  ##### End Aliases setup #####
  ```
---
#### Setup terminal colors
* First :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Terminal Color enabling #####
  eval "`dircolors`"
  force_color_prompt=yes
  alias ls='ls --color=auto'
  ##### End Terminal Color enabling #####
  ```
---
#### Setup autoclear RamCache
> https://github.com/microsoft/WSL/issues/4166
* First :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Auto clear Ram Cache #####
  printf "%s" "Clearing ram-cache ..."
  su -c "echo 3 >'/proc/sys/vm/drop_caches' && printf '\n%s\n' 'Clearing ram-cache OK'" root
  ##### End Auto clear Ram Cache #####
  ```
---
#### Setup autoload for Apache2
* First :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Auto load Apache2 #####
  if [ $(service apache2 status | grep -v grep | grep 'apache2 is not running ... failed!' | wc -l) != 0 ]
  then
    su -c "printf '\n%s\n' 'Starting Apache2.4 service...' && service apache2 start && printf '%s\n' 'Started Apache2.4 service.'" root
  else
    su -c "printf '\n%s\n' 'Apache2.4 service already started.'" root
  fi
  ##### End Auto load Apache2 #####
  ```
---
#### Setup autoload for MySQL
* First :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Auto load MySQL #####
  if [ $(service mysql status | grep -v grep | grep 'MariaDB is stopped..' | wc -l) != 0 ]
  then
    su -c "printf '\n%s\n' 'Starting mysql9.1 service...' && service mysql start && printf '%s\n' 'Started mysql9.1 service.'" root
  else
    su -c "printf '\n%s\n' 'Mysql9.1 service already started.'" root
  fi
  ##### End Auto load MySQL #####
  ```
---
#### Setup Wakatime API
> https://wakatime.com/terminal#install-bash
* First :
  ```bash
  $ pip3 install wakatime
  $ cd /root/
  $ git clone https://github.com/gjsheep/bash-wakatime.git
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Wakatime enabling #####
  source /root/bash-wakatime/bash-wakatime.sh
  ##### End Wakatime enabling #####
  ```
* Visit https://wakatime.com/settings/account and copy your API KEY
* Then :
  ```bash
  $ emacs /root/.wakatime.cfg
  ```
* Write inside :
  ```conf
  [settings]
  api_key = $API_KEY
  ```
---
#### Setup Powerline Go
> https://github.com/justjanne/powerline-go
* First :
  ```bash
  $ apt-get install golang -y
  $ go get -u github.com/justjanne/powerline-go
  $ emacs /root/.bashrc
  ```
* Write inside :
  ```bash
  ##### Start Powerline Go enabling #####
  GOPATH=/root/go
  function _update_ps1() {
    PS1="$($GOPATH/bin/powerline-go -error $?)"
  }
  if [ "$TERM" != "linux" ] && [ -f "$GOPATH/bin/powerline-go" ]; then
    PROMPT_COMMAND="_update_ps1; $PROMPT_COMMAND"
  fi
  ##### End Powerline Go enabling #####
  ```
* Then visit : https://github.com/adam7/delugia-code/releases, download `Delugia.Nerd.Font.Complete.ttf` and install it on Windows
---
#### Setup Archey4
> https://github.com/HorlogeSkynet/archey4
* First :
  ```bash
  $ pip3 install archey4
  $ emacs /etc/archey4/config.json
  ```
* Write inside :
  ```json
  {
    "allow_overriding": true,
    "suppress_warnings": true,
    "entries": {
      "User": true,
      "Hostname": true,
      "Model": false,
      "Distro": true,
      "Kernel": true,
      "Uptime": true,
      "WindowManager": false,
      "DesktopEnvironment": false,
      "Shell": true,
      "Terminal": true,
      "Packages": true,
      "Temperature": false,
      "CPU": true,
      "GPU": false,
      "RAM": true,
      "Disk": true,
      "LAN_IP": true,
      "WAN_IP": true
    },
    "colors_palette": {
      "use_unicode": true
    },
    "default_strings": {
      "no_address": "No Address",
      "not_detected": "Not detected",
      "virtual_environment": "Virtual Environment",
      "bare_metal_environment": "Bare-metal Environment"
    },
    "ip_settings": {
      "lan_ip_max_count": 2,
      "wan_ip_v6_support": false
    },
    "limits": {
      "ram": {
        "warning": 33.3,
        "danger": 66.7
      },
      "disk": {
        "warning": 50,
        "danger": 75
      }
    },
    "temperature": {
      "char_before_unit": "°",
      "use_fahrenheit": false
    },
    "timeout": {
      "ipv4_detection": 1,
      "ipv6_detection": 1
    }
  }
  ```
* Then :
  ```bash
  $ emacs /root/.bashrc
  ```
* Write inside
  ```bash
  ##### Start Archey enabling #####
  archey
  ##### End Archey enabling #####
  ```
<br/>

## Create Apache2 VirtualHost
* First :
  ```bash
  $ emacs /etc/apache2/sites-available/sub.domain.ext.conf
  ```
* Write inside :
  ```conf
  <VirtualHost *:80>
    ServerName sub.domain.ext
    #ServerAlias sub2.domain.ext only if necessary
    DocumentRoot /var/www/sub.domain.ext/

    ErrorLog /var/log/apache2/sub.domain.ext.error.log
    CustomLog /var/log/apache2/sub.domain.ext.access.log combined
  </VirtualHost>
  ```
* Then :
  ```bash
  $ a2ensite sub.domain.ext
  $ service apache2 restart
  ```
<br/>

## Create user

### MySQL user
* First :
  ```bash
  $ mysql -u root -p
  ```
  * Then, in SQL :
  ```SQL
  > CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
  > CREATE DATABASE database;
  > GRANT ALL PRIVILEGES ON database.* TO 'user'@'localhost';
  > FLUSH PRIVILEGES;
  > exit;
  ```

### Unix user
* First :
  ```bash
  $ NEWUSER=nomprenom
  $ useradd -m -s /bin/bash $NEWUSER
  $ chmod 755 /home/$NEWUSER
  $ rm /home/$NEWUSER/.bashrc
  $ usermod -g www-data $NEWUSER
  $ emacs /home/$NEWUSER/.bash_profile
  ```
* Write inside :
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
* Then :
  ```bash
  $ chown root:root /home/$NEWUSER/.bash_profile
  $ chmod 755 /home/$NEWUSER/.bash_profile
  $ ssh-keygen
  ```
* If user uses Windows system, or will use FileZilla (or any program that use .ppk key files) :
  * Download /home/$NEWUSER/.ssh/id_rsa
  * Download PuTTY
  * Install PuTTYgen and open it
  * click on `Conversions` > `Import key`
  * type passphrase
  * Export private key to .ppk format
* Finally :
  ```bash
  $ cat /home/$NEWUSER/.ssh/id_rsa.pub >> /home/$NEWUSER/.ssh/authorized_keys
  $ chmod -R go= /home/$NEWUSER/.ssh/
  $ chown -R $NEWUSER:$NEWUSER /home/$NEWUSER/.ssh/
  ```

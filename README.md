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
#### Setup Github GPG Key
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
* Then visit : https://github.com/adam7/delugia-code/releases,<br />
  Download `Delugia.Nerd.Font.Complete.ttf` and install it on Windows
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

## Create new user
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

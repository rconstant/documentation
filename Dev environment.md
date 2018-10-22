## Install debian instructions

### Edit .bashrc

    function pc {
      [ -d .git ] && git name-rev --name-only @
    }
    export PS1='\[\033[1;31m\]\u\[\033[0m\]@\[\033[1;34m\]\h\[\033[0m\]:\w \e[36m$(pc)\e[m\$ '

    export LS_OPTIONS='--color=auto'
    eval "`dircolors`"
    alias ls='ls $LS_OPTIONS'
    alias ll='ls $LS_OPTIONS -l'
    alias l='ls $LS_OPTIONS -lA'

### Install softwares

    apt-get update

    apt-get install vim
    apt-get install git
    apt-get install curl
    apt-get install unzip
    apt-get install mysql-client

### Dev environment
#### Nginx

    sudo sh -c 'echo "deb http://nginx.org/packages/mainline/debian/ stretch nginx"' > /etc/apt/sources.list.d/nginx.list

    wget http://nginx.org/keys/nginx_signing.key

    apt-key add nginx_signing.key

    apt-get update

    apt-get install nginx

#### PHP 7.2

    apt-get install apt-transport-https lsb-release ca-certificates
    
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg

    sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

    apt-get update

    apt install nginx php7.2 php7.2-common php7.2-cli php7.2-fpm php7.2-mysql php7.2-xml php7.2-curl php7.2-mbstring php7.2-zip php7.2-intl php7.2-bcmath php7.2-json

#### NodeJS 10

    wget -qO- https://deb.nodesource.com/setup_10.x | sudo -E bash -

    apt-get install -y nodejs

    apt-get install -y build-essential

#### Composer

    curl -sS https://getcomposer.org/installer | php

    mv composer.phar /usr/local/bin/composer

    chmod +x /usr/local/bin/composer

    composer global require hirak/prestissimo

### Problem resolve
#### Remove memory limit for Composer update

    php -d memory_limit=-1 /usr/local/bin/composer update

#### Erreur WSL

Erreur

    Installing, this may take a few minutes...
    WslRegisterDistribution failed with error: 0x800703fa
    Error: 0x800703fa Illegal operation attempted on a registry key that has been marked for deletion.

    Press any key to continue...

How to resolve

    net stop "LxssManager" & sc start "LxssManager"
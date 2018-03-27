---
layout: post
title: "Ruby On Rails, ubuntu setup from scratch"
category: "cheatsheet"
date: 2018-03-26 10:28:07
---

## Basic setup

### root
- install utilities

```bash
apt-get install git htop
```

- install Oh My Zsh

```bash
apt-get install zsh
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

- configure vim

```zsh
wget https://gist.githubusercontent.com/bassochette/c64b4919a2207f15efd7d4dce04490d0/raw/143f0ce01a96c513e87565fcdddc61017c107d41/.vimrc
```

- configure ssh
- setup firewall

- create app user

```zsh
adduser app
```

- configure vim for app user

```zsh
wget https://gist.githubusercontent.com/bassochette/c64b4919a2207f15efd7d4dce04490d0/raw/143f0ce01a96c513e87565fcdddc61017c107d41/.vimrc
```

- install Node Js 8.X

```zsh
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
apt-get update
apt-get install -y nodejs
node -v
```

- install Ruby

```zsh
apt-get update
apt-get install build-essential libssl-dev libyaml-dev libreadline-dev openssl curl git-core zlib1g-dev bison libxml2-dev libxslt1-dev libcurl4-openssl-dev libsqlite3-dev sqlite3
wget http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.4.tar.gz
tar -xvzf ruby-2.5.0.tar.gz
cd ruby-2.5.0
./configure
make
make install
ruby -v
```

- install rails

```zsh
gem install rails
```

- install Apache

```zsh
apt-get install apache2
```

- install passenger

```
apt-get install -y dirmngr gnupg
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
apt-get install -y apt-transport-https ca-certificates
sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger xenial main > /etc/apt/sources.list.d/passenger.list'
apt-get update
apt-get install -y libapache2-mod-passenger
a2enmod passenger
service apache2 restart
```

- install postgresql

```zsh
apt-get install postgres postgres-contrib libpq-dev
su - postgres
```

- create app user

```
createuser --interactive
createdb app
exit
gem install pg
```

## Application setup

- clone sources

```
git clone repo_url
```

- install deps

```
bundle install --path vendor/bundle
```

- configure db connection

```
echo "app:
  adapter: postgresql
  encoding: unicode
  database: app
  pool: 5
  username: app
  password: awesomepasswordyo
  host: 127.0.0.1
" > config/database.yml

```

## Vhost setup

```
<VirtualHost *:80>
    ServerName ambroisie.io
    ServerAlias app.ambroisie.io
    ServerAdmin julien@ambroisie.io
    DocumentRoot /home/app/ambroisie/public
    RailsEnv app
    SetEnv RAILS_ENV production
    SetEnv SECRET_KEY_BASE secret
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory "/home/app/ambroisie/public">
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```

## SSL

- Install certbot

```
apt-get update
apt-get install software-properties-common
add-apt-repository ppa:certbot/certbot
apt-get update
apt-get install python-certbot-apache
```

- Run interactive setup

```
certbot --apache
```


## sources
- [Download Ruby](https://www.ruby-lang.org/en/downloads/)
- [Basic .vimrc](https://gist.github.com/bassochette/c64b4919a2207f15efd7d4dce04490d0)
- [Oh My ZSH](https://github.com/robbyrussell/oh-my-zsh)
- [certbot](https://certbot.eff.org/lets-encrypt/ubuntuxenial-apache)
- [How To Install and Use PostgreSQL on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04)
- [Installing Node.js via package manager](https://nodejs.org/en/download/package-manager/)
- [How To Deploy a Rails App with Passenger and Apache on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-rails-app-with-passenger-and-apache-on-ubuntu-14-04)
- [](https://www.digitalocean.com/community/tutorials/how-to-set-up-let-s-encrypt-certificates-for-multiple-apache-virtual-hosts-on-ubuntu-14-04)
- [Installing Passenger + Apache](https://www.phusionpassenger.com/library/install/apache/install/oss/xenial/)
- [How To Setup Ruby on Rails with Postgres](https://www.digitalocean.com/community/tutorials/how-to-setup-ruby-on-rails-with-postgres)
- [How to switch databases in psql?
](https://stackoverflow.com/questions/3949876/how-to-switch-databases-in-psql?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

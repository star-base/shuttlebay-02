Shuttlebay Superleggera
==========

Shuttlebay Superleggera is a preconfigured Vagrant Box with a full array of LAMP Stack features to get you up and running with Vagrant in no time. This is a lightweight version of Shuttlebay https://github.com/star-base/shuttlebay

A lot of PHP websites and applications don’t require much server configuration or overhead at first. This box should have all your needs for doing basic development so you don’t have to worry about configuring Vagrant and you can simply focus on your code.

No provisioning tools or setup is really even required with Shuttlebay Superleggera. Since everything is packaged into the box, running “vagrant” is super fast, you’ll never have to worry about your environment breaking with updates, and you won’t need Internet to code.


## What and Why

The idea of the Superleggera varient of Shuttlebay **All I really want is PHP 5.6 and a bunch of modules with zero hassle or overhead**.

## Features

### System Stuff

- Ubuntu 14.04 LTS (Trusty Tahr)
- PHP 5.6
- Ruby 2.2.x
- Vim
- Git
- cURL
- GD and Imagick
- Composer
- Beanstalkd
- Node
- NPM
- Mcrypt

### Database Stuff
- MySQL
- PostgreSQL
- SQLite

### Caching Stuff

- Redis
- Memcache and Memcached

### Node Stuff

- Grunt
- Bower
- Yeoman
- Gulp
- Browsersync
- PM2

### Laravel Stuff

- Laravel Installer
- Laravel Envoy
- Blackfire Profiler

### Other Useful Stuff

- No Internet connection required
- PHP Errors turned on
- Laravel and WordPress ready
- Operating System agnostic
- Goodbye XAMPP / WAMP


## Get Started

* Download and Install [Vagrant][1]
* Download and Install [VirtualBox][2]
* Clone the Shuttlebay Superleggera [GitHub Repository](https://github.com/star-base/shuttlebay-superleggera)
* Run ``` vagrant up ```
* Access Your Project at  [http://192.168.33.10/][4]

## Basic Vagrant Commands


### Start or resume your server
```bash
vagrant up
```

### Pause your server
```bash
vagrant suspend
```

### Delete your server
```bash
vagrant destroy
```

### SSH into your server
```bash
vagrant ssh
```



## Database Access

### MySQL 

- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox

### PostgreSQL

- Hostname: localhost or 127.0.0.1
- Username: root
- Password: root
- Database: scotchbox
- Port: 5432


### MongoDB

- Hostname: localhost
- Database: scotchbox
- Port: 27017


## SSH Access

- Hostname: 127.0.0.1:2222
- Username: vagrant
- Password: vagrant

## Mailcatcher

Just do:

```
vagrant ssh
mailcatcher --http-ip=0.0.0.0
```

Then visit:

```
http://192.168.33.10:1080
```


## Updating the Box

Although not necessary, if you want to check for updates, just type:

```bash
vagrant box outdated
```

It will tell you if you are running the latest version or not, of the box. If it says you aren't, simply run:

```bash
vagrant box update
```


## Setting a Hostname

If you're like me, you prefer to develop at a domain name versus an IP address. If you want to get rid of the some-what ugly IP address, just add a record like the following example to your computer's host file.

```bash
192.168.33.10 whatever-i-want.dev
```

Or if you want "www" to work as well, do:

```bash
192.168.33.10 whatever-i-want.dev www.whatever-i-want.dev
```

Technically you could also use a Vagrant Plugin like Vagrant Hostmanager to automatically update your host file when you run Vagrant Up. However, the purpose of Scotch Box is to have as little dependencies as possible so that it's always working when you run "vagrant up".


## Configuration

You may want to change some of the out-of-the-box configurations for
the various parts that come with Shuttlebay Superleggera. To do so, `vagrant ssh`
into the box, and edit the appropriate file.  For example, to change
PHP settings:

    vagrant ssh
    sudo vim /etc/php5/apache2/conf.d/user.ini

Note that the changes that you make will be for the current running
Scotch Box only.  If you `vagrant destroy` and then `vagrant up` your
box again, these manual configuration changes will be lost.

If you prefer to automate your configuration changes so that you can
destroy and re-create boxes as needed, Vagrant allows you to create a
"provision script" that runs as part of `vagrant up`.  See the
[Vagrant
documentation](https://docs.vagrantup.com/v2/getting-started/provisioning.html)
for notes.  For example, you could add the following line to your
Vagrantfile under the `config.vm.hostname = "shuttlebay"` line:

    config.vm.provision :shell, path: "bootstrap.sh"

and then create `bootstrap.sh` with the following content in the same
directory as the Vagrantfile:

    #!/bin/bash
    # Disable Zend OPcache
    sed -i 's/;opcache.enable=0/opcache.enable=0/g' /etc/php5/apache2/php.ini

This script will be run each time you `vagrant up`, and it can be run
on an already-up box using `vagrant provision`.

## PHP7 Install Instructions

```
sudo apt-get update
sudo add-apt-repository ppa:ondrej/php
sudo apt-get install php7.0
sudo apt-get update
sudo apt-get install php7.0-mysql libapache2-mod-php7.0
sudo a2dismod php5
sudo a2enmod php7.0
sudo apachectl restart
```



 [1]: https://www.vagrantup.com/downloads.html
 [2]: https://www.virtualbox.org/wiki/Downloads
 [3]: http://www.sequelpro.com/
 [4]: http://192.168.33.10/
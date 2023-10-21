<div align="center">
    <a href="https://teddysun.com/700.html" target="_blank">
        <img alt="LCMP" src="https://github.com/teddysun/lcmp/raw/master/conf/lcmp.png">
    </a>
</div>

## Description

LCMP is a powerful bash script for the installation of Caddy2 + MariaDB + PHP and so on.

You can install Caddy2 + MariaDB + PHP in a smaller memory VPS by yum command, Just need to input numbers to choose what you want to install before installation.

And all things will be done in a few minutes.

## Supported System

- Enterprise Linux 7 (CentOS 7, RHEL 7)
- Enterprise Linux 8 (CentOS 8, RHEL 8, Rocky Linux 8, AlmaLinux 8)
- Enterprise Linux 9 (CentOS 9, RHEL 9, Rocky Linux 9, AlmaLinux 9)
- Debian 10
- Debian 11
- Debian 12
- Ubuntu 20.04
- Ubuntu 22.04

## System requirements

- Hard disk space: 5GB
- RAM: 512MB
- An internet connection is required
- Correct repository
- User: root

## Supported Software

- Caddy 2
- MariaDB 10.11
- PHP-7.4, PHP-8.0, PHP-8.1, PHP-8.2

## Installation

- If your server's OS system: Enterprise Linux 7/8/9
```bash
yum -y install wget git
git clone https://github.com/teddysun/lcmp.git
cd lcmp
chmod 755 *.sh
./lcmp.sh 2>&1 | tee lcmp.log
```

- If your server's OS system: Debian/Ubuntu
```bash
apt-get -y install wget git
git clone https://github.com/teddysun/lcmp.git
cd lcmp
chmod 755 *.sh
./lcmp.sh 2>&1 | tee lcmp.log
```

## Upgrade

- If your server's OS system: Enterprise Linux 7/8/9
```bash
yum update -y caddy
yum update -y MariaDB-*
yum update -y php-*
# Change PHP directory's group for Caddy again if you upgraded PHP version
chown root:caddy /var/lib/php/session
chown root:caddy /var/lib/php/wsdlcache
chown root:caddy /var/lib/php/opcache
```

- If your server's OS system: Debian/Ubuntu
```bash
apt-get install --only-upgrade -y caddy
apt-get install --only-upgrade -y mariadb-*
# for example: php_ver=[8.0|8.1|8.2]
php_ver="8.2"
apt-get install --only-upgrade -y php${php_ver}-*
```

## Uninstall

- If your server's OS system: Enterprise Linux 7/8/9
```bash
yum remove -y caddy
yum remove -y MariaDB-*
yum remove -y php-*
```

- If your server's OS system: Debian/Ubuntu
```bash
apt-get remove -y caddy
apt-get remove -y mariadb-*
# for example: php_ver=[8.0|8.1|8.2]
php_ver="8.2"
apt-get remove -y php${php_ver}-*
```

## Default Location

| Caddy Location             | Path                                        |
|----------------------------|---------------------------------------------|
| Web root location          | /data/www/default                           |
| Main Configuration File    | /etc/caddy/Caddyfile                        |
| Sites Configuration Folder | /etc/caddy/conf.d/                          |

| MariaDB Location           | Path                                        |
|----------------------------|---------------------------------------------|
| Data Location              | /var/lib/mysql                              |
| my.cnf File (rpm)          | /etc/my.cnf                                 |
| my.cnf File (deb)          | /etc/mysql/my.cnf                           |

| PHP Location               | Path                                        |
|----------------------------|---------------------------------------------|
| php-fpm File (rpm)         | /etc/php-fpm.d/www.conf                     |
| php-fpm File (deb)         | /etc/php/${php_ver}/fpm/pool.d/www.conf     |
| php.ini File (rpm)         | /etc/php.ini                                |
| php.ini File (deb)         | /etc/php/${php_ver}/fpm/php.ini             |

## Process Management

| Process     | Command                                                    |
|-------------|------------------------------------------------------------|
| PHP (rpm)   | systemctl [start\|stop\|status\|restart] php-fpm           |
| PHP (deb)   | systemctl [start\|stop\|status\|restart] php${php_ver}-fpm |
| Caddy       | systemctl [start\|stop\|status\|restart] caddy             |
| MariaDB     | systemctl [start\|stop\|status\|restart] mariadb           |

## License

Copyright (C) 2023 Teddysun

Licensed under the [GPLv3](LICENSE) License.

Description
===========
LCMP is a powerful bash script for the installation of Caddy2 + PHP + MariaDB and so on.

You can install Caddy2 + PHP + MariaDB in a smaller memory VPS by yum command, Just need to input numbers to choose what you want to install before installation.

And all things will be done in a few minutes.

Supported System
===============
- Enterprise Linux 7 (CentOS 7, RHEL 7)
- Enterprise Linux 8 (CentOS 8, RHEL 8, Rocky Linux 8, AlmaLinux 8)
- Enterprise Linux 9 (CentOS 9, RHEL 9, Rocky Linux 9, AlmaLinux 9)

System requirements
===================
- Hard disk space: 5GB
- RAM: 512MB
- An internet connection is required
- Correct repository
- User: root

Supported Software
==================
- Caddy 2
- MariaDB 10.11
- PHP-7.4, PHP-8.0, PHP-8.1, PHP-8.2

Installation
============
```bash
yum -y install wget git
git clone https://github.com/teddysun/lcmp.git
cd lcmp
chmod 755 *.sh
./lcmp.sh 2>&1 | tee lcmp.log
```

Upgrade
=======
```bash
yum update -y caddy
yum update -y MariaDB-*
yum update -y php-*
# Change PHP directory's group for Caddy again
chown root.caddy /var/lib/php/session
chown root.caddy /var/lib/php/wsdlcache
chown root.caddy /var/lib/php/opcache
```

Uninstall
=========
```bash
yum remove -y caddy
yum remove -y MariaDB-*
yum remove -y php-*
```

Default Location
================
| Caddy Location             | Path                                     |
|----------------------------|------------------------------------------|
| Web root location          | /data/www/default                        |
| Main Configuration File    | /etc/caddy/Caddyfile                     |
| Sites Configuration Folder | /etc/caddy/conf.d/                       |

| MariaDB Location           | Path                                     |
|----------------------------|------------------------------------------|
| Data Location              | /var/lib/mysql                           |
| my.cnf Configuration File  | /etc/my.cnf                              |

| PHP Location               | Path                                     |
|----------------------------|------------------------------------------|
| php-fpm Configuration File | /etc/php-fpm.d/www.conf                  |
| php.ini Configuration File | /etc/php.ini                             |

Process Management
==================
| Process     | Command                                                 |
|-------------|---------------------------------------------------------|
| PHP         | systemctl [start\|stop\|status\|restart] php-fpm        |
| Caddy       | systemctl [start\|stop\|status\|restart] caddy          |
| MariaDB     | systemctl [start\|stop\|status\|restart] mariadb        |

License
=======
Copyright (C) 2023 Teddysun

Licensed under the [GPLv3](LICENSE) License.

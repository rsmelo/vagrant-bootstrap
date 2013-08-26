VagrantBootstrap for Symfony2
=============================

A simple provisioning Vagrant bootstrap to be ready for PHP/MySQL development.
This is a Symfony2 bootstrap with ~100ms with Symfony Standard. Tested with the version 2.3.3.

## Step 1 :

Please, edit your AppKernel.php, replace "appname" with your application name (it must be the same of the `APPLICATION_NAME` parameter in the file "parameters.sh" !). For more information about this fix, please read : http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html
```php
<?php

class AppKernel extends Kernel
{
    // ...

    public function getCacheDir()
    {
        if (in_array($this->environment, array('dev', 'test'))) {
            return '/dev/shm/appname/cache/' .  $this->environment;
        }

        return parent::getCacheDir();
    }

    public function getLogDir()
    {
        if (in_array($this->environment, array('dev', 'test'))) {
            return '/dev/shm/appname/logs';
        }

        return parent::getLogDir();
    }
}
```

## Step 2 :

Your application must be in the `/vagrant` shared folder.

That's all !


If you have using Symfony2, please see the branch named `symfony2`.

## Features :

- Apache 2 with rewrite mod and ready VHOST
- PHP 5.x (last stable release, now 5.5.x. You can choose older stable version in bootstrap.sh, see PHP part)
- PHP packages : php5-cli php5-mysql php5-curl php5-mcrypt php5-gd php-pear php5-xdebug php5-intl
- MariaDB (MySQL) with custom database and root remote access (no password)
- Some essential packages : build-essential git-core vim curl

## Forwarded ports :

- 22 (SSH) > 2222
- 80 (HTTP) > 8000
- 3306 (MySQL) > 33060

## Bootstrap and box parameters

### Bootstrap parameters

You need to edit some custom parameters in the file ".vagrant_bootstrap/parameters.sh" :

Database parameters :
- `DATABASE_NAME` : your database name. If empty, no database will be created.
- `DATABASE_ROOT_HOST` : allowed host for the ROOT user. Put "localhost" (by default), for localhost access only (more secure in prod, for example), 10.0.2.2 for you host access only or "%" for remote access (usefull to access to the database from your remote database software).

PHP parameters :
- `PHP_TIMEZONE` : the PHP timezone (default: "UTC"). Check possible values here : http://php.net/manual/en/timezones.php

## Other stuff

Do not forget to run the command `vagrant reload` with `--no-provision` option to disable provisioning.

Feel free to fork me !

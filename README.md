<p align="center"><img src="https://github.com/laravel/sail/raw/HEAD/art/logo.svg" alt="Logo Laravel Sail"></p>

<p align="center">
    <a href="https://packagist.org/packages/laravel/sail">
        <img src="https://img.shields.io/packagist/dt/laravel/sail" alt="Total Downloads">
    </a>
    <a href="https://packagist.org/packages/laravel/sail">
        <img src="https://img.shields.io/packagist/v/laravel/sail" alt="Latest Stable Version">
    </a>
    <a href="https://packagist.org/packages/laravel/sail">
        <img src="https://img.shields.io/packagist/l/laravel/sail" alt="License">
    </a>
</p>

## Introduction

Sail provides a Docker powered local development experience for Laravel that is compatible with macOS, Windows (WSL2), and Linux. Other than Docker, no software or libraries are required to be installed on your local computer before using Sail. Sail's simple CLI means you can start building your Laravel application without any previous Docker experience.

> **Note**  
> This fork has been modified to include some extra ease-of-life features like an Nginx proxy for custom domains, Imagick support etc.

## Official Documentation

Documentation for Sail can be found on the [Laravel website](https://laravel.com/docs/sail).

## Unofficial Documentation

Before installing, you need to configure composer to use our remote repository:

```bash
composer config repositories.repolaserred composer https://repo.laser.red
```

Now you can install Sail as normal by running:

```bash
composer require laravel/sail --dev
```

When configuring a new site and running `php artisan sail:install`, set the `--host` option to the domain you'd like to use (without the protocol), otherwise it will default to [laravel.test](http://laravel.test). Don't forget to also add your chosen domain (or the default) to your hosts file and point it to `127.0.0.1`. For example:

```bash
php artisan sail:install --with=mysql,redis,mailhog --host=my-site.local
```

## Aero Configuration

Ensure you have the correct version of the Aero CLI tool installed globally:

```bash
composer global require aerocommerce/cli
```

In order to create a new aero project you will need first to register it on AGORA 

[agora.aerocommerce.com]( https://agora.aerocommerce.com).

Go the projects tab and create a new project giving it a name and a domain , once this has been completed you should be presented with a username and password.

Now you can install Aero:

```bash
aero new --no-install --next
```
_The `--next` flag is currently required to get the latest Laravel base._

> **Note**  
> If this responds with `command not found` it likely means you don't have your global composer path in exported in your `$PATH`. You can find this path with `composer config --list --global | grep home` and then prepend that path so you have something like `~/.composer/vendor/bin/aero new --no-install --next`

Now you can install Sail as normal by running:

```bash
composer require laravel/sail --dev
```

_This may show an error message about tables not being found, ignore this as we just haven't installed aero yet._

When setting up Sail, ensure you add the `--aero` flag so it adds the correct services: 

```bash
php artisan sail:install --aero --host=my-site.local
```

Depending on your base Laravel version, check that the docker-compose.yml is provisioned with the correct php version for the application by altering the lines, e.g. 

`context: ./vendor/laravel/sail/runtimes/8.2`

and 

`image: sail-8.2/app `

Update your `.env` to include:
```Dotenv
DB_HOST=mysql
REDIS_HOST=redis
ELASTICSEARCH_HOST=elasticsearch
CACHE_DRIVER=redis
SESSION_DRIVER=redis
```

If the app service env variable hasn't been created, add it to the env file and name it after what is on line 4 in your docker-compose.yml e.g.

`APP_SERVICE=aero-test.local`

> **Note**  
> From this point onwards all composer commands will need to be run inside the container I.E sail composer install, not composer install.


Now you have all the defaults configured, you can start Sail:
```bash
sail up -d
```

Run aero install from inside our container
```bash
sail artisan aero:install
```

When prompted, enter the username and password from the Project you set up in agora, this will install a fresh instance of aero.

In order to set up a theme for our project we will need to install some prerequisites

```bash
sail composer require aerocommerce/theme-ui aerocargo/listing-collections aerocommerce/account-area aerocommerce/components
```

Now install the skeleton theme and answer yes when prompted to activate:

```bash
sail artisan theme:install aero/skeleton --name=skeleton
```

This should now have installed a skeleton theme you can now work from.

If you would like to import some test products into your application for testing purposes you can run the following command.

```bash
sail artisan aero:import:products:csv https://aero-data.s3.eu-west-2.amazonaws.com/furniture.csv
```

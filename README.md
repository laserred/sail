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
composer global require aerocommerce/cli:dev-master#c31fe1bf53c05860ad45342106d028677f2bfa52
```

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

Depending on your base Laravel version, amend your `docker-compose.yml` to use relevant PHP runtime, e.g. `context: ./vendor/laravel/sail/runtimes/7.4`

Update your `.env` to include:
```Dotenv
DB_HOST=mysql
REDIS_HOST=redis
ELASTICSEARCH_HOST=elasticsearch
CACHE_DRIVER=redis
SESSION_DRIVER=redis
AERO_THEME=vendor/<your-theme-name>
```

Now you have all the defaults configured, you can start Sail:
```bash
sail up -d
```

And once sail has launched you can complete the Aero installation:
```bash
sail artisan aero:install
```

You can optionally install a base theme:
```bash
sail composer require aerocommerce/theme-ui aerocargo/listing-collections aerocommerce/account-area aerocommerce/components
```

Or create your theme from the base theme:
```bash
sail artisan theme:build vendor/<your-theme-name> --config=vendor/aerocommerce/theme-ui/config/phantom.yml
```

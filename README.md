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

This fork has been modified to include some extra ease-of-life features like an Nginx proxy for custom domains, Imagick support etc.

We should always require the `release` branch which is ours, that fixes some issues with pulling using their tags. This branch will always contain the latest updates.

## Unofficial Documentation

Add this to your project's `composer.json`:

```
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/laserred/sail.git"
        }
    ]
```

Make sure the version required is `"laravel/sail": "dev-release"` - add this by doing `composer require laravel/sail:dev-release`.

During `php artisan sail:install` set the option `--host` to the domain you'd like to use (without the protocol), otherwise it will default to [laravel.test](http://laravel.test). Don't forget to also add your chosen domain (or the default) to your hosts file and point it to `127.0.0.1`. For example:

`php artisan sail:install --with=mysql,redis,mailhog --host=host-name.local`

## How to configure for Aero

First ensure you have the correct version of the aero cli tool installed globally.
`composer global require aerocommerce/cli:dev-master#c31fe1bf53c05860ad45342106d028677f2bfa52`

Find out where your globally installed composer packages are (mine live in ~/.config/composer/vendor/) and then either alias the aero command in your shell or run it from the path you found above.

` ~/.config/composer/vendor/aerocommerce/cli/aero new --no-install --next`

Amend your newly created composer.json to include this repository as explained above, and then `composer require laravel/sail:dev-feature-aero` (TODO: this will need changing to `dev-release` once merged).

This may show an error message about tables not being found, ignore this, we just haven't installed aero yet.
Set up sail with `php artisan sail:install --aero` the `--aero` flag will ensure elasticsearch is included in your docker compose.

Amend your docker compose to use the php 7.4 runtime ` context: ./vendor/laravel/sail/runtimes/7.4`
Amend your .env to include:

```
DB_HOST=mysql
REDIS_HOST=redis
ELASTICSEARCH_HOST=elasticsearch
CACHE_DRIVER=redis
SESSION_DRIVER=redis
```

You can now `sail up -d`

Once sail has launched you can run the aero install with `sail artisan aero:install`

## Official Documentation

Documentation for Sail can be found on the [Laravel website](https://laravel.com/docs/sail).

## License

Laravel Sail is open-sourced software licensed under the [MIT license](LICENSE.md).

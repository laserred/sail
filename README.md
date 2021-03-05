<p align="center"><img src="/art/logo.svg" alt="Logo Laravel Sail"></p>

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

This Fork has been modified to support the new M1 chips on Apple devices.

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

During `php artisan sail:install` set the option `--host` to the domain you'd like to use (without the protocol), otherwise it will default to [laravel.test](http://laravel.test). Don't forget to also add your chosen domain (or the default) to your hosts file and point it to `127.0.0.1`.

## Official Documentation

Documentation for Sail can be found on the [Laravel website](https://laravel.com/docs/sail).

## License

Laravel Sail is open-sourced software licensed under the [MIT license](LICENSE.md).

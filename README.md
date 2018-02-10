# Cascading Config

[![Build Status](https://travis-ci.org/phanan/cascading-config.svg?branch=master)](https://travis-ci.org/phanan/cascading-config)
[![Dependency Status](https://gemnasium.com/phanan/cascading-config.svg)](https://gemnasium.com/phanan/cascading-config)
[![License](https://poser.pugx.org/phanan/cascading-config/license.svg)](https://packagist.org/packages/phanan/cascading-config)

A simple package that brings the cascading configuration system back into Laravel 5 and its sister project, Lumen.

## Requirements

* Laravel 5, or
* Lumen >=5.1

## Features
* Laravel-4 style cascading config (can't believe I'm writing this)
* [Nested configuration](https://github.com/laravel/framework/commit/fee982004a795058ab6a66e1600c11aac6748acf) is fully supported

## Installation

First, require `weidacat/cascading-config` into your `composer.json` and run `composer update`:

```
composer require "weidacat/cascading-config:dev-master"
```

An environment-based configuration directory should have a name with this format `config.{APP_ENV}`, and reside in the same directory as the default `config` dir. For Laravel, `php artisan vendor:publish`
will create a sample directory for your `local` environment. For Lumen, you'll have to create the directories manually.

Your application structure now should have something like this:

```
config
├── app.php
├── auth.php
├── cache.php
├── compile.php
├── database.php
├── mail.php
└── ...
config.local
├── app.php
├── auth.php
├── cache.php
├── mail.php
└── nested
    └── app.php
```

Fill the configuration into your environment-based config directory (`config.local`, `config.staging`, `config.production`), just like what you've always done in Laravel 4,

## Usage

### For Laravel

1. Add the package's service provider class into `config/app.php`:

    ``` php
    'providers' => [
        /*
         * ...
         */
        App\Providers\AppServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,

        Weidacat\CascadingConfig\CascadingConfigServiceProvider::class,
    ],
    ```
    
1.  Call `config($key)`

### For Lumen

1. Register the service provider class in `bootstrap/app.php`:

    ```php
    // $app->register(App\Providers\AppServiceProvider::class);
    // $app->register(App\Providers\EventServiceProvider::class);
    $app->register(Weidacat\CascadingConfig\CascadingConfigServiceProvider::class);
    ```

## Notes

Because of the way `array_merge_recursive()` works, a config key with value being an indexed (non-associative) array (for instance, `app.providers`) will have the value's items overridden. See [#6](https://github.com/phanan/cascading-config/issues/6) for more details on this behavior, and how to work around it.

## License

MIT © [Phan An](http://phanan.net)

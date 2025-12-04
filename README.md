Exception reporter for laravel-admin
======================

This tool stores the exception information into the database and provides a developer-friendly web interface to view the exception information.

[![Packagist](https://img.shields.io/packagist/l/php-panel/ladmin-ext-reporter.svg?maxAge=2592000)](https://packagist.org/packages/php-panel/ladmin-ext-reporter)
[![Total Downloads](https://img.shields.io/packagist/dt/php-panel/ladmin-ext-reporter.svg?style=flat-square)](https://packagist.org/packages/php-panel/ladmin-ext-reporter)
[![Pull request welcome](https://img.shields.io/badge/pr-welcome-green.svg?style=flat-square)]()

## Screenshot

![laravel-admin_exceptions](https://user-images.githubusercontent.com/1479100/30947042-0f667d9a-a43a-11e7-99c3-cf0fe236fedd.png)

## Installation 

```
$ composer require php-panel/ladmin-ext-reporter -vvv

$ php artisan vendor:publish --tag=laravel-admin-reporter

$ php artisan migrate --path=vendor/laravel-admin-ext/reporter/database/migrations

$ php artisan admin:import reporter
```

Open `app/Exceptions/Handler.php`, call `Reporter::report()` inside `report` method:
```php
<?php

namespace App\Exceptions;

use Ladmin\Reporter\Reporter;
use Exception;
use Illuminate\Auth\AuthenticationException;
use Illuminate\Validation\ValidationException;
use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;

class Handler extends ExceptionHandler
{
    ...

    public function report(Exception $exception)
    {
        if ($this->shouldReport($exception)) {
            Reporter::report($exception);
        }

//        parent::report($exception);
    }
    
    ...

}
```

Open `http://localhost/admin/exceptions` to view exceptions.

License
------------
Licensed under [The MIT License (MIT)](LICENSE).

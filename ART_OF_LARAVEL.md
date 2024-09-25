<!-- TABLE OF CONTENTS -->

## Art Of Laravel

- [Controller Tips](#controller-tips)

  - [Single Action Controllers](#Single-Action-Controllers)
- [Contact](#contact)


  <!-- UPDATE NODE -->

## Controller Tips

### Single Action Controllers

If you dedicate an entire controller class to that single action, you can accomplish this, you may define a single `__invoke` method within the controller:

```php
<?php

namespace App\Http\Controllers;

class HomeController extends Controller
{
    /**
     * Show only homepage.
     */
    public function __invoke()
    {
        // ...
    }
}
```

When registering routes for single action controllers, you do not need to specify a controller method. Instead, you may simply pass the name of the controller to the router:

```php
use App\Http\Controllers\HomeController;

//Before defining a __invoke method
Route::get('/home-page',[ HomeController::class, 'METHOD_NAME']);

//After defining a __invoke method
Route::get('/home-page', HomeController::class);
```

You may generate an invokable controller by using the --invokable option of the make:controller Artisan command:

```php
php artisan make:controller ProvisionServer --invokable
```

## Contact

Md Hafizul Islam - [hafizpustice05@gmail.com](mailto:hafizpustice05@gmail.com)

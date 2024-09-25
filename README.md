<!-- TABLE OF CONTENTS -->

## Art Of Laravel

- [Controller Tips](#controller-tips)
  - [Single Action Controllers](#Single-Action-Controllers)
- [Wehre Clause](#where-clause)
  - [Before](#before)
  - [After](#after)
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
     * Only define a single action.
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

Since that previous-syntax is rather verbose, Laravel provides additional, `__invoke` methods that use conventions to provide a better developer experience.

You may generate an invokable controller by using the --invokable option of the make:controller Artisan command:

```php
php artisan make:controller ProvisionServer --invokable
```

## Before

```php
Customer::select('id', 'name', 'email')
          ->whereJsonContains('address->post_code', $postCode)
          ->whereJsonContains('address->country', $country)
          ->get();

```

## After

```php
Customer::select('id', 'name', 'email')->where(
            function ($query) use ($country, $postCode) {
                return $query
                    ->whereJsonContains('address->post_code', $postCode)
                    ->whereJsonContains('address->country', $country);
            }
        )->get();
```

## Contact

Md Hafizul Islam - [hafizpustice05@gmail.com](mailto:hafizpustice05@gmail.com)

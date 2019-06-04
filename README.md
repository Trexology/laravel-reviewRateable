[![Latest Stable Version](https://poser.pugx.org/trexology/reviewrateable/v/stable)](https://packagist.org/packages/trexology/reviewrateable)
[![Total Downloads](https://poser.pugx.org/trexology/reviewrateable/downloads)](https://packagist.org/packages/trexology/reviewrateable)
[![Latest Unstable Version](https://poser.pugx.org/trexology/reviewrateable/v/unstable)](https://packagist.org/packages/trexology/reviewrateable) [![License](https://poser.pugx.org/trexology/reviewrateable/license)](https://packagist.org/packages/trexology/reviewrateable)

# Laravel ReviewRateable
ReviewRateable system for laravel 5.*

## Installation

First, pull in the package through Composer.

```js
composer require trexology/reviewrateable
```

And then include the service provider within `app/config/app.php`. (Skip this step if you are on Laravel 5.5 or above)

```php
'providers' => [
    Trexology\ReviewRateable\ReviewRateableServiceProvider::class
];
```

At last you need to publish and run the migration.
```
php artisan vendor:publish --provider="Trexology\ReviewRateable\ReviewRateableServiceProvider" && php artisan migrate
```

-----

### Setup a Model
```php
<?php

namespace App;

use Trexology\ReviewRateable\Contracts\ReviewRateable;
use Trexology\ReviewRateable\Traits\ReviewRateable as ReviewRateableTrait;
use Illuminate\Database\Eloquent\Model;

class Post extends Model implements ReviewRateable
{
    use ReviewRateableTrait;
}
```

### Create a rating
```php
$user = User::first();
$post = Post::first();

$rating = $post->rating([
    'title' => 'Some title',
    'body' => 'Some body', //optional
    'anonymous' => 1, //optional
    'rating' => 5,
], $user);

dd($rating);
```

### Update a rating
```php
$rating = $post->updateRating(1, [
    'title' => 'new title',
    'body' => 'new body', //optional
    'anonymous' => 1, //optional
    'rating' => 3,
]);
```

### Delete a rating:
```php
$post->deleteRating(1);
```

### Fetch the average rating:
````php
$post->averageRating()
````

or

````php
$post->averageRating(2) //round to 2 decimal place
````

### Count total rating:
````php
$post->countRating()
````

### Count rating meta (Count and Avg):
````php
$post->ratingMeta()
````

or

````php
$post->ratingMeta(2) //round to 2 decimal place
````

### Fetch the rating percentage.
This is also how you enforce a maximum rating value.
````php
$post->ratingPercent()

$post->ratingPercent(10)); // Ten star rating system
// Note: The value passed in is treated as the maximum allowed value.
// This defaults to 5 so it can be called without passing a value as well.
````

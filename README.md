[![Build Status](https://travis-ci.org/Trexology/rating.svg?branch=master)](https://travis-ci.org/Trexology/rating)
[![Latest Stable Version](https://poser.pugx.org/Trexology/rating/v/stable.svg)](https://packagist.org/packages/Trexology/rating) [![License](https://poser.pugx.org/Trexology/rating/license.svg)](https://packagist.org/packages/Trexology/rating)

[![Total Downloads](https://poser.pugx.org/Trexology/rating/downloads.svg)](https://packagist.org/packages/Trexology/rating)

# Laravel Rating
Rating system for laravel 5

## Installation

First, pull in the package through Composer.

```js
composer require Trexology/rating
```

And then include the service provider within `app/config/app.php`.

```php
'providers' => [
    Trexology\Rating\RatingServiceProvider::class
];
```

At last you need to publish and run the migration.
```
php artisan vendor:publish --provider="Trexology\Rating\RatingServiceProvider" && php artisan migrate
```

-----

### Setup a Model
```php
<?php

namespace App;

use Trexology\Rating\Contracts\Rating;
use Trexology\Rating\Traits\Rating as RatingTrait;
use Illuminate\Database\Eloquent\Model;

class Post extends Model implements Rating
{
    use RatingTrait;
}
```

### Create a rating
```php
$user = User::first();
$post = Post::first();

$rating = $post->rating([
    'title' => 'Some title',
    'body' => 'Some body',
    'rating' => 5,
], $user);

dd($rating);
```

### Update a rating
```php
$rating = $post->updateRating(1, [
    'title' => 'new title',
    'body' => 'new body',
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

### Fetch the rating percentage. 
This is also how you enforce a maximum rating value.
````php
$post->ratingPercent()

$post->ratingPercent(10)); // Ten star rating system
// Note: The value passed in is treated as the maximum allowed value.
// This defaults to 5 so it can be called without passing a value as well.
````
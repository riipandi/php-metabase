# PHP Metabase
Library to embed [Metabase](http://www.metabase.com/) frames. Forked from [ipeevski/metabase-php](https://github.com/ipeevski/metabase-php)

## Installation
- Install via composer: `composer require riipandi/php-metabase`
- Go to Metabase and enable embedding - https://{metabase_url}/admin/settings/embedding_in_other_applications
- Note down the Metabase base url and the Embedding secret key

## Basic usage
First, you need to find the dashboard or question you want to embed. 
Note down the id - it would be at the end of the URL (for example https://{metabase_url}/dashboard/1?date=past26weeks

Note the integer after /dashboard/ - that's the ID of the dashboard.
Also note the GET parameters at the end of the url - those are parameters you might want 
to pass to the dashboard too.


```php
<?php

include 'vendor/autoload.php';

$metabaseUrl = '[metabase_url]';      // The url of the metabase installation
$metabaseKey = '[metabase_key]';      // The metabase secret embed key
$dashboardId = 1;                     // The id of the dashboard (from the url)
$params = ['date' => 'past26weeks'];  // Any parameters to pass to the dashboard (optional)

$metabase = new \Metabase\Embed($metabaseUrl, $metabaseKey);

// Generate the HTML to create an iframe with the embedded dashboard
echo $metabase->dashboardIframe($dashboardId, $params);
```

## Using Laravel

Create config file at `confog/metabase.php`

```php
<?php

return [
    'url' => env('METABASE_URL', 'http://localhost:3000'),
    'key' => env('METABASE_KEY'),
]
```

```php
<?php

$metabaseUrl = config('metabase.url');    // The url of the metabase installation
$metabaseKey = config('metabase.key');    // The metabase secret embed key
$dashboardId = 1;                         // The id of the dashboard (from the url)
$params = ['date' => 'past26weeks'];      // Any parameters to pass to the dashboard (optional)

$metabase = new \Metabase\Embed($metabaseUrl, $metabaseKey);

// Generate the HTML to create an iframe with the embedded dashboard
echo $metabase->dashboardIframe($dashboardId, $params);
```

## License

MIT: [https://aris.mit-license.org/](https://aris.mit-license.org/)

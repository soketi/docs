# Laravel Broadcasting

For [Laravel Broadcasting](https://laravel.com/docs/8.x/broadcasting) it's even easier, just replace the `pusher` configuration from `config/broadcasting.php` with the following code.

The variables will be injected from the [frontend configuration](../client-configuration/laravel-echo.md).

```php
'connections' => [
    
    // ...
    
    'pusher' => [
        'driver' => 'pusher',
        'key' => env('PUSHER_APP_KEY', 'app-key'),
        'secret' => env('PUSHER_APP_SECRET', 'app-secret'),
        'app_id' => env('PUSHER_APP_ID', 'app-id'),
        'options' => [
            'host' => env('PUSHER_HOST', '127.0.0.1'),
            'port' => env('PUSHER_PORT', 6001),
            'scheme' => env('PUSHER_SCHEME', 'http'),
            'encrypted' => true,
            'useTLS' => env('PUSHER_SCHEME') === 'https',
        ],
    ],
],
```

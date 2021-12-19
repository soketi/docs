# Laravel Broadcasting

When using [Laravel's event broadcasting](https://laravel.com/docs/8.x/broadcasting) feature within your application, soketi is even easier to configure. First, replace the default `pusher` configuration in your application's `config/broadcasting.php` file with the following configuration:

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

### Self-signed Certificates

Due to implementation changes in the Pusher PHP SDK, releases of the SDK since the `6.0` release do not support `curl_options`; therefore, self-signed SSL certificates will fail certificate validation since certificate verification cannot be disabled. To bypass SSL Verification, you must use Pusher PHP SDK version `5.0.3`.

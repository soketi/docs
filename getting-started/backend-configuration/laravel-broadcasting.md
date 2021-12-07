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

### Self-signed Certificates

For Pusher package `5.0.3` and beyond, you can use `curl_options` to bypass CA verification in case you're using self-signed certificates:

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
        'curl_options' => [
            CURLOPT_SSL_VERIFYHOST => env('PUSHER_VERIFY_CERT', 1),
            CURLOPT_SSL_VERIFYPEER => env('PUSHER_VERIFY_CERT', 1),
        ],
    ],
],
```

{% hint style="warning" %}
Due to implementation upgrades for the Pusher package, the Pusher package version `6.0` and above does not support `curl_options` anymore, and self-signed SSL certificates are forced validation. To be able to bypass SSL Verification, use the Pusher package version `5.0.3` until further notice.
{% endhint %}

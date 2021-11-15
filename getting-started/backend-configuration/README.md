# 💻 Backend Configuration

Keep in mind that this backend configuration is a PHP example, but this applies to all Pusher-maintained backend clients.

```php
use Pusher\Pusher;

$pusher = new Pusher('app-key', 'app-secret', 'app-id', [
    'host' => '127.0.0.1',
    'port' => 6001,
    'scheme' => 'http',
    'encrypted' => true,
    'useTLS' => false,
]);
```

{% hint style="info" %}
For [SSL configurations](../ssl-configuration.md), set the `scheme` to `http` and `useTLS` to `true`
{% endhint %}

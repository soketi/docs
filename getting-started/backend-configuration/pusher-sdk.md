# Pusher SDK



The backend configuration of your real-time messaging infrastructure will depend on the language of your application. However, in this example we will demonstrate configuration the Pusher PHP SDK to interact with soketi, which should be similar to the configuration of server-side Pusher SDKs in other languages:

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
To configure the client for [SSL](../ssl-configuration.md), you should set the `scheme` option to `http` and the `useTLS` option to `true`
{% endhint %}

### Encrypted Private Channels

[Pusher Encrypted Private Channels](https://pusher.com/docs/channels/using\_channels/encrypted-channels/) are also supported, meaning that for private channels, you can encrypt your data symmetrically at both your client and backend applications, soketi NOT knowing at all what the actual data is set, acting just like a deliverer.

```php
use Pusher\Pusher;

$pusher = new Pusher('app-key', 'app-secret', 'app-id', [
    // ...
    'encryptionMasterKeyBase64' => '...',  // generate this with, e.g. 'openssl r
]);
```

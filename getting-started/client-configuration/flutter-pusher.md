# Flutter Pusher

In Flutter we have the [dart_pusher_channels](https://pub.dev/packages/dart_pusher_channels) package that works perfectly with Soketi.

The package is not official from Pusher (company), but the package is cross-platform and always updated.

```dart
const hostOptions = PusherChannelsOptions.fromHost(
      scheme: 'ws',
      host: 'you_soketi_ip',
      key: 'app-key',
      shouldSupplyMetadataQueries: true,
      metadata: PusherChannelsOptionsMetadata.byDefault(),
      port: 6001,
    );
 
final client = PusherChannelsClient.websocket(
    options: hostOptions,
    connectionErrorHandler: (exception, trace, refresh) async {
        print(exception);
        refresh();
    });

final String? deviceId = 'soketi';
String token = base64.encode(utf8.encode(deviceId.toString()));

final myPrivateChannel = client.privateChannel(
    "private-users.$deviceId",
    authorizationDelegate:
        EndpointAuthorizableChannelTokenAuthorizationDelegate
            .forPrivateChannel(
    authorizationEndpoint: Uri.parse("your_api/auth"),
    headers: {"Authorization": "Bearer $token"},
    ),
);
final StreamSubscription connectionSubs =
    client.onConnectionEstablished.listen((_) {
    myPrivateChannel.subscribeIfNotUnsubscribed();
});

client.connect();

StreamSubscription<ChannelReadEvent> somePrivateChannelEventSubs =
    myPrivateChannel.bind('messages').listen((event) {
    print(event.data);
    print(event.channel.name);
});
```

The code above contains a working example of connecting to a private channel, hence the 'authorizationEndpoint'. On public channels this parameter is completely optional.

{% hint style="info" %}
For a complete example you can visit [Examples](https://pub.dev/packages/dart_pusher_channels/example).
{% endhint %}

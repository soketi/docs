# ⚛ User Authentication

Pusher allows you to [authenticate the users attempting to connect to the websockets](https://pusher.com/docs/channels/server\_api/authenticating-users/) before deciding if the server should keep the connection or not. In this sense, Soketi allows you to authenticate the users of your app too. It also takes care of [authorized connections](https://pusher.com/docs/channels/using\_channels/authorized-connections/) automatically.

All apps have this feature disabled by default, and you can decide for each app if this should be enabled or not.

[Read more about the app management where you can enable the user authentication.](../app-management/introduction.md)

By default, when the app has user authentication enabled, Soketi disconnects unauthenticated or unauthorized connections in 30 seconds. However, you can change this duration using the following environment variable:

```bash
# 5 seconds timeout
SOKETI_USER_AUTHENTICATION_TIMEOUT=5000
```

#### Send message to specific user ID

With the help of the new HTTP API endpoint, Soketi can also allow you to send a message specific to an user id. This feature is implemented on all SDKs and you can see a JS sample below.

The SDKs namings differ, so ensure you use the latest SDK version for your language.

```javascript
pusher.sendToUser('1', 'order-shipped', {
    id: 'A2BQW2',
    items: [{
        name: 'Iphone',
    }],
});
```

#### Terminate specific user's connections

Soketi supports terminating a user's connections after it was authenticated. It stays in sync with Pusher's protocol and most of the SDKs are already implementing a method for this functionality. Ensure you use the latest SDK version for your language.

```javascript
pusher.terminateUserConnections('1');
```

# 📐 AWS Lambda trigger

{% hint style="info" %}
This feature is available starting with version 0.15
{% endhint %}

soketi allows you to configure Lambda triggers instead of setting up your own HTTP server. This comes in handy when you want to process the backend, but you want to reduce the complexity of creating and maintaining a backend to catch webhooks.

### Configure Lambda triggers

To configure an app to send Lambda, you may specify the Lambda function details for the SDK in your app's `webhooks` field.&#x20;

In the HTTP app webhooks, you could have configured them like this:

```json
{
    "url": "string",
    "event_types": ["string", ...]
}
```

If you specify a `lambda_function` instead of the `url`, you can enable the Lambda invocation:

```json
{
    "lambda_function": "my-function",
    "event_types": ["string", ...]
}
```

### Setting credentials for the AWS client

Under the hood, AWS SDK is used and it requires authentication. AWS has [detailed documentation with many ways to set credentials for the Lambda client](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html). soketi uses the same convention so you are free to set your credentials from the `.aws` folder, from environment variables, from the EC2 profile, as they will be automatically injected.

For advanced usage, like when you want to register Lambdas from another AWS accounts, you can configure the credentials by yourself from the webhook definition through a `lambda` key:

```json
{
    "lambda_function": "my-function",
    "event_types": ["string", ...],
    "lambda": {
        "client_options": {
            "region": "eu-central-1",
            "credentials": {
                "accessKeyId": "...",
                "secretAccessKey": "..."
            }
        }
    }
}
```

{% hint style="warning" %}
Keep in mind that hard-coding credentials can bring security risks. In case you deploy soketi within an EC2 instance or an ECS container, you should not specify credentials and, instead, give your EC2 instances or your ECS containers the permission to invoke your lambdas via their service role, as credentials will be automatically injected and recognized by soketi.
{% endhint %}

### Example Lambda code

Below you will find an example Lambda code that can be used to catch incoming events:

```javascript
exports.handler = async ({ payload, headers }) => {
    const { createHmac } = require('crypto');

    // Create webhook HMAC so that we know if the message comes from the real server.
    let computedEventHmac = createHmac('sha256', process.env.SOKETI_SECRET)
        .update(JSON.stringify(payload))
        .digest('hex');

    // Compute the payload (message) HMAC with the injected secret in the environment variables
    // and see if the sent header matches it. If not, the message must have been tampered with and you
    // should not process it by any means.
    if (typeof headers['X-Pusher-Signature'] === undefined || computedEventHmac !== headers['X-Pusher-Signature']) {
        return;
    }

    payload.events.forEach(({ name, channel }) => {
        if (name === 'channel_occupied') {
            console.log(channel + ' is now occupied.');
        }
    });
};
```

As you can see, it's really easy to implement Lambda and catch webhooks.

{% hint style="danger" %}
Please note that you should always check if the HMAC of the payload matches the one received via `headers`. If it does not match, it's possible that the data has been tampered with and you should never process the message.
{% endhint %}

{% hint style="info" %}
The secret can be injected in the [Environment Variables](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html) section from your Lambda function.
{% endhint %}

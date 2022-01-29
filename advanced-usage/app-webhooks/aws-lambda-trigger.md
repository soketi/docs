# 📐 AWS Lambda trigger

{% hint style="info" %}
This feature is available starting with soketi version 0.15
{% endhint %}

soketi allows you to configure Lambda triggers instead of setting up your own HTTP server to handle webhooks.

### Configure Lambda triggers

To configure an app to send webhook information to Lambda, you may specify the Lambda function details in your app's `webhooks` field. Instead of the typical HTTP webhook handler which looks like the following:

```json
{
    "url": "string",
    "event_types": ["string", ...]
}
```

You may specify a `lambda_function` instead of a `url`:

```json
{
    "lambda_function": "my-function-arn",
    "region": "us-east-1",
    "event_types": ["string", ...]
}
```

{% hint style="info" %}
You must specify the `region` when defining a `lambda_function`.
{% endhint %}

### Setting credentials for the AWS client

Under the hood, the AWS SDK is used to invoke Lambda functions and it requires authentication. AWS has [detailed documentation with many ways to set credentials for the Lambda client](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html). soketi uses the same convention, so you are free to set your credentials within the `.aws` folder, using environment variables, or using an EC2 profile.

If you would like to specify the AWS account credentials directly in your webhook configuration, you may add a "lambda" key to the webhook configuration with additional configuration options:

```json
{
    "lambda_function": "my-function",
    "event_types": ["string", ...],
    "lambda": {
        "region": "eu-central-1",
        "client_options": {
            "credentials": {
                "accessKeyId": "...",
                "secretAccessKey": "..."
            }
        }
    }
}
```

{% hint style="warning" %}
Keep in mind that hard-coding AWS credentials into your webhook configuration can increase security risks. If you deploy soketi within an EC2 instance or an ECS container, you should not specify credentials within the webhook definition and instead give your EC2 instances or your ECS containers the permission to invoke your Lambda via their service role, as the credentials will be automatically injected and recognized by soketi.
{% endhint %}

### IAM Policy Permissions

To be able to invoke the Lambda, the IAM User or Instance Role should have the following permissions:

* `lambda:InvokeFunction`

### Example Lambda code

Below you will find an example Lambda function implementation that can be used to handle incoming events:

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

{% hint style="danger" %}
Note that you should always check if the HMAC of the payload matches the one received via the `headers`. If it does not match, it's possible that the data has been tampered with and you should discard the message.
{% endhint %}

{% hint style="info" %}
The soketi secret in the example above can be injected into the Lambda using the [Environment Variables](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html) section of your Lambda function's management dashboard.
{% endhint %}

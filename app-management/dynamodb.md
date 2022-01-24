# 👾 DynamoDB

soketi supports connecting to a DynamoDB table (global or regional) to retrieve app data. This driver is highly efficient for this purpose since no strong consistency is needed and there are two indexes that will be used (`AppId` and `AppKey`).

Of course, soketi requires your DynamoDB table to use a predefined schema so that soketi knows how to retrieve your app data. The following DynamoDB schema is written in Javascript, but may be translated to other formats as needed:

```javascript
ddb.createTable({
    // ...

    AttributeDefinitions: [
        {
            AttributeName: 'AppId',
            AttributeType: 'S',
        },
        {
            AttributeName: 'AppKey',
            AttributeType: 'S',
        },
    ],

    KeySchema: [{
        AttributeName: 'AppId',
        KeyType: 'HASH',
    }],

    GlobalSecondaryIndexes: [{
        IndexName: 'AppKeyIndex',
        KeySchema: [{
            AttributeName: 'AppKey',
            KeyType: 'HASH',
        }],
        Projection: {
            ProjectionType: 'ALL',
        },
        ProvisionedThroughput: {
            // ...
        },
    }],

    // ...
});
```

Inserting data into this table would look like the following:

```javascript
const params = {
    TableName: 'apps',
    Item: {
        AppId: { S: 'app-id' },
        AppKey: { S: 'app-key' },
        AppSecret: { S: 'app-secret' },
        MaxConnections: { N: '-1' },
        EnableClientMessages: { B: 'false' },
        Enabled: { B: 'true' },
        MaxBackendEventsPerSecond: { N: '-1' },
        MaxClientEventsPerSecond: { N: '-1' },
        MaxReadRequestsPerSecond: { N: '-1' },
        Webhooks: { S: '[]' },
    },
};

ddb.putItem(params);
```

{% hint style="info" %}
Note that the "Webhooks" field is stored as a JSON-encoded string.
{% endhint %}

{% hint style="info" %}
AWS has [detailed documentation with many ways to define credentials for the DynamoDB client](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html). soketi uses the same conventions, so you are free to define your AWS credentials in the `.aws` folder, environment variables, or from an EC2 / ECS profile.
{% endhint %}

### Environment Variables

The following environment variables are used to control the behavior of the DynamoDB app driver:

| **Name**                        | Default     | Possible values | Description                                                                                             |
| ------------------------------- | ----------- | --------------- | ------------------------------------------------------------------------------------------------------- |
| `APP_MANAGER_DYNAMODB_TABLE`    | `apps`      | Any string      | The table to pull the app data from.                                                                    |
| `APP_MANAGER_DYNAMODB_REGION`   | `us-east-1` | Any AWS region  | The DynamoDB region the table was deployed to. For global tables, you may choose any region.            |
| `APP_MANAGER_DYNAMODB_ENDPOINT` | `''`        | Any URL         | The endpoint used to connect to DynamoDB. May be used for testing or for local DynamoDB configurations. |

### Limits on an app-by-app basis

This feature is truly optional. Your items in DynamoDB can have the following new fields:

```javascript
MaxPresenceMembersPerChannel: { N: '-1' },
MaxPresenceMemberSizeInKb: { N: '-1' },
MaxChannelNameLength: { N: '-1' },
MaxEventChannelsAtOnce: { N: '-1' },
MaxEventNameLength: { N: '-1' },
MaxEventPayloadInKb: { N: '-1' },
MaxEventBatchSize: { N: '-1' },
```

Not setting any of the above fields will ignore the setting, and will fallback to the limits associated [with the server-level declared defaults](../rate-limiting-and-limits/events-and-channels-limits.md).

Existing apps running on `<0.29.0` will still work even if you don't have these fields added after the migration to `0.29.0`. You should add these fields to keep your database up-to-date or to have the choice to, later on, imply limits to your apps.

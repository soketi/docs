# 👾 DynamoDB

pWS supports connecting to a DynamoDB table \(either global or regional one\) to pull data from it.

This driver has proven to be highly efficient for the apps table since no strong consistency is needed and there are two indexes which the app will be pulled with. For this, a defined schema should be used, just like the SQL drivers.

The following example is written in Javascript, but the schema remains the same:

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

// Inserting would look like this:
const params = {
    TableName: 'apps',
    Item: {
        AppId: { S: 'app-id' },
        AppKey: { S: 'app-key' },
        AppSecret: { S: 'app-secret' },
        MaxConnections: { N: '-1' },
        EnableClientMessages: { B: 'false' },
        MaxBackendEventsPerSecond: { N: '-1' },
        MaxClientEventsPerSecond: { N: '-1' },
        MaxReadRequestsPerSecond: { N: '-1' },
        Webhooks: { S: '[]' },
    },
};

ddb.putItem(params);
```

**It's worth noting that the Webhooks field is stored as a JSON-encoded string.**


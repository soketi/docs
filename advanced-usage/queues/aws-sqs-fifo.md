# ⛓ AWS SQS FIFO

Starting with soketi 0.30, you may now use AWS's SQS FIFO queues to process webhooks and other background tasks.

### Creating the queue

The driver works strictly with the High-Throughput FIFO Queue mode. Below you will find an example command line to create a FIFO Queue for soketi using the AWS CLI.

The recommended values can be adjusted according to your needs, such as `MessageRetentionPeriod`, but these are optimal for this soketi's use case.

```bash
aws sqs create-queue --queue-name test.fifo \
  --attributes='{
    "FifoQueue": "true",
    "ContentBasedDeduplication": "true",
    "DeduplicationScope": "messageGroup",
    "FifoThroughputLimit": "perMessageGroupId",
    "MessageRetentionPeriod": "3600",
    "ReceiveMessageWaitTimeSeconds": "1",
    "VisibilityTimeout": "5"
  }'
```

{% hint style="warning" %}
Keep in mind that the `DeduplicationScope` and `FifoThroughputLimit` should be set as below since the queues may be processed on an app ID and queue type basis for extreme throughput. The `ContentBasedDeduplication` should be true.
{% endhint %}

### Caveats

#### IAM Permissions

Make sure that when setting the IAM policies for the authentication user or instance role, you  will include the following IAM permissions:

* `sqs:ReceiveMessage`
* `sqs:SendMessage`

#### Visibility Timeout too low

Since the webhooks are used for now for sending HTTP requests or Lambda invocations, make sure that the total process time is lower than the Visibility Timeout duration, otherwise, another consumer can claim the message after the duration.

### Environment Variables

| Name                       | Default   | Possible values           | Description                                                                                                           |
| -------------------------- | --------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `QUEUE_SQS_REGION`         | us-east-1 | Any string                | The region in which the SQS queue is deployed.                                                                        |
| `QUEUE_SQS_CLIENT_OPTIONS` | `''`      | Any JSON-formatted string | A JSON-formatted string with additional options to pass to the `new SQS()` function.                                  |
| `QUEUE_SQS_URL`            | `''`      | Any string                | The URL of the queue. It has to be ending in `.fifo` (ex: `https://sqs.eu-central-1.amazonaws.com/xxxx/myqueue.fifo`) |
| `QUEUE_SQS_ENDPOINT`       | `''`      | Any string                | Optional string to test SQS locally or manually define the endpoint for the SQS API.                                  |

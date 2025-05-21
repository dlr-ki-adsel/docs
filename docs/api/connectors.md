# Connectors

Just like you manage Connectors through the website, you can also manage them via the API. This section describes exactly how to do this. All endpoints described here are protected.

## Create Connectors

You can create a Connector by sending a `POST` request to `/connectors/<your-chosen-connector-name>`.

The payload must be provided as a `JSON`. If you intend on only using the `API` you can simply send `{}` as payload. However, if you want to also use this Connector via the website you need to provide correct storage credentials in the payload.

After a successful request the Connector will be created and begin to start up.

### AmazonS3

For explanations on the exact values you need to provide, please refer to the website documentation.

```json
{
    "endpointOverride": "<endpoint>",
    "region": "<region>",
    "accessKeyIdRead": "<username-read>",
    "secretAccessKeyRead": "<password-read>",
    "accessKeyIdWrite": "<username-write>",
    "secretAccessKeyWrite": "<password-write>",
    "bucketName": "<bucket-name>"
}
```

### AzureStorage

For explanations on the exact values you need to provide, please refer to the website documentation.

```json
{
    "blobstoreEndpointTemplate": "<endpoint-template>",
    "accountKeyRead": "<username-read>",
    "accountNameRead": "<password-read>",
    "accountKeyWrite": "<username-write>",
    "accountNameWrite": "<password-write>",
    "containerName": "<container-name>"
}
```

Note: Azure Storage is currently not usable due to a bug in the Connector.

## Edit Connectors

Simlarly to creating a Connector you can edit a Connector by sending a `PUT` request to `/connectors/<connector-name>`. The payload you need to provide here is exactly the same as for creating a Connector. After a successful request the Connector will restart using the newly provided configuration.

## Get Connectors

You can get a list of all your Connectors by sending a `GET` request to `/connectors`. If you want to get only a specific Connector you can send a `GET` request to `/connectors/<connector-name>`.

## Start and Stop Connectors

To start and stop a Connector you can send a `GET` request to `/connectors/<connector-name>/start` and `/connectors/<connector-name>/stop` respectively.

## Fail Connectors

In some cases a Connector might be stuck in some unwanted state because of a bug. If that is the case you can get the Connector into the `FAILED` state by sending a `GET` request to `/connectors/<connector-name>/fail`. From there you can either stop or delete the Connector. Note, however, that this does not necessarily mitigate the bug.

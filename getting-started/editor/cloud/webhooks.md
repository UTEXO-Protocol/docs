# Webhooks

The Utexo Cloud supports webhooks to notify users about events in their nodes. This document explains how to use webhooks and provides example payloads.

**Adding a Webhook Endpoint**

You can add a webhook endpoint to your node by editing the node's settings:

1. Navigate to your node and click **Settings**.
2. Locate the field named **Webhook URL**.
3. Enter the endpoint where you'd like to send requests.
4. Note down your public key from the settings, as it will be used to verify requests.

**Adding a Webhook When Creating a Node**

When creating a new node via the API, you can provide a **Webhook URL** in the settings. This allows  to send webhook notifications to your specified endpoint. You can update this URL later through the node's settings if needed.

**Retrieve the Public Key**

To verify webhook requests, retrieve the public key from the following URL: [https://cloud-api.thunderstack.org/api/webhook-public-key](https://cloud-api.thunderstack.org/api/webhook-public-key)

This public key is used to validate the `X-ThunderStack-Signature` header included in each webhook event.

**How Webhooks Work**

When an event is triggered, ThunderStack sends a **POST** request to your webhook endpoint. The request includes:

1. A **JSON payload** with details about the event.
2. A header named `X-ThunderStack-Signature` containing a digital signature created with ThunderStack's private key.

**Verification Steps**

1. **Validate the Signature**: Use the public key to verify the `X-ThunderStack-Signature` header.
2. **Validate the Payload**: Ensure the `nodeId` in the payload matches the expected node or endpoint.

**Payload Schema**

The JSON payload sent to your webhook endpoint has the following structure:

```
jsonCopy code{
  "eventType": "NODE_STATUS_UPDATED", 
  "eventTimestamp": "2024-11-06T12:00:00Z", 
  "details": {
    "nodeId": "your-node-id",
    "status": "RUNNING"
  },
  "nodeId": "your-node-id"
}
```

**Status Values**

The `status` field within `details` can have one of the following values:

* **RUNNING**: The node is running.
* **STARTING**: The node is starting.
* **PAUSED**: The node is paused.
* **FAILED**: The node has failed.
* **IN\_PROGRESS**: An operation is currently in progress.

**Security Considerations**

1. **Use HTTPS**: Always use HTTPS for your webhook endpoint to ensure data security during transit.
2. **Signature Verification**: Validate the `X-ThunderStack-Signature` header using the public key.
3. **Payload Validation**: Ensure the `nodeId` field matches the expected node.

This ensures secure, reliable, and real-time notifications for your nodes.

**Example Webhook Handler**

Here’s an example of a webhook handler in JavaScript/TypeScript:

```
javascriptCopy codeimport * as crypto from 'crypto';

// Main function to handle webhook events
export async function handleWebhookEvent(request) {
    // Extract the signature and body
    const receivedSignature = request.headers['x-thunderstack-signature'] || request.headers['X-ThunderStack-Signature'];
    const body = typeof request.body === 'string' ? request.body : JSON.stringify(request.body);

    // Retrieve the public key for signature verification
    const publicKey = 'YOUR_PUBLIC_KEY_HERE';

    // Create a verifier to validate the signature using the public key
    const verify = crypto.createVerify('RSA-SHA256');
    verify.update(body);
    verify.end();

    // Validate the signature
    const isValid = verify.verify(publicKey, receivedSignature, 'base64');
    if (!isValid) {
        console.error('Invalid signature');
        return {
            statusCode: 403,
            body: JSON.stringify({ message: 'Forbidden - Invalid Signature' })
        };
    }

    // Handle the validated webhook event here
    console.log('Valid webhook event received');
    return {
        statusCode: 200,
        body: JSON.stringify({ message: 'Webhook event processed successfully' })
    };
}
```

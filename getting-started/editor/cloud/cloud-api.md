---
description: REST API reference for managing Cloud nodes.
---

# Cloud API

## Cloud API

Manage Cloud nodes over a REST JSON API.

### Base URL

`https://cloud-api.thunderstack.org`

### Authentication

All endpoints use bearer auth.

```bash
export CLOUD_API_TOKEN="<your_token>"
```

Each request must include:

```bash
-H "Authorization: Bearer ${CLOUD_API_TOKEN}"
```

{% hint style="info" %}
Examples below use `curl` and show paths relative to the base URL.
{% endhint %}

### List nodes

**GET** `/api/nodes`

Returns all nodes and their build history.

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes"
```

Example response:

```json
{
  "nodes": [
    {
      "nodeId": "<node_id>",
      "name": "<name>",
      "network": "regtest",
      "status": "RUNNING",
      "initialized": true,
      "invoke_url": "<url>",
      "settings": { "webhookUrl": "<url>" },
      "builds": [
        {
          "buildNumber": 1,
          "buildStatus": "SUCCESS",
          "buildComplete": true,
          "timestamp": "<iso8601>"
        }
      ]
    }
  ]
}
```

### Create a node

**POST** `/api/nodes`

Body fields:

* `name` (string, required)
* `network` (string, required): `regtest` or `testnet`
* `settings` (object, optional)
  * `webhookUrl` (string, optional)

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "my-node",
    "network": "regtest",
    "settings": { "webhookUrl": "https://example.com/webhooks/thunderstack" }
  }' \
  "https://cloud-api.thunderstack.org/api/nodes"
```

Example response:

```json
{
  "data": {
    "nodeId": "<node_id>",
    "name": "my-node",
    "network": "regtest",
    "status": "STARTING"
  },
  "message": "<message>"
}
```

### Get a node

**GET** `/api/nodes/{id}`

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>"
```

### Destroy a node

**DELETE** `/api/nodes`

Body fields:

* `destroyNodeId` (string, required)

{% hint style="warning" %}
This endpoint expects a JSON body on a `DELETE` request. Some HTTP clients require an explicit `-X DELETE`.
{% endhint %}

```bash
curl -s -X DELETE \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{ "destroyNodeId": "<node_id>" }' \
  "https://cloud-api.thunderstack.org/api/nodes"
```

Example response:

```json
{ "message": "<message>" }
```

### Webhooks: public key

**GET** `/api/webhook-public-key`

Returns the public key used to verify webhook signatures.

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/webhook-public-key"
```

Example response:

```json
{ "data": "<public_key>" }
```

### RLN images: latest version

**GET** `/api/nodes/latest-rln-image`

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/latest-rln-image"
```

Example response:

```json
{ "data": "<rln_version>" }
```

### RLN images: upgrade node

**POST** `/api/nodes/{id}/upgrade`

```bash
curl -s -X POST \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/upgrade"
```

Example response:

```json
{ "message": "<message>" }
```

### Node settings: update

**POST** `/api/nodes/{id}/settings`

Use this to change node settings like `webhookUrl`.

```bash
curl -s -X POST \
  -H "Authorization: Bearer ${THUNDERSTACK_API_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{ "settings": { "webhookUrl": "https://example.com/webhooks/thunderstack" } }' \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/settings"
```

Example response:

```json
{ "message": "<message>" }
```

### Node lifecycle: start

**POST** `/api/nodes/{id}/start`

```bash
curl -s -X POST \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/start"
```

Example response:

```json
{}
```

### Node lifecycle: stop

**POST** `/api/nodes/{id}/stop`

```bash
curl -s -X POST \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/stop"
```

Example response:

```json
{}
```

### Logs: trigger export

**POST** `/api/nodes/{id}/logs`

Starts a log export job for a node.

```bash
curl -s -X POST \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/logs"
```

Example response:

```json
{ "taskId": "<task_id>" }
```

### Logs: get download URLs

**GET** `/api/nodes/{id}/logs?taskId={taskId}`

```bash
curl -s \
  -H "Authorization: Bearer ${CLOUD_API_TOKEN}" \
  "https://cloud-api.thunderstack.org/api/nodes/<node_id>/logs?taskId=<task_id>"
```

Example response:

```json
{ "data": ["<presigned_url>"] }
```

# Batching requests

> Example

```shell
$ curl https://api.twistapp.com/api/v1/batch \
  -d token=0123456789abcdef0123456789abcdef01234567 \
  -d requests='[{"method": "GET", "url": "https://api.twistapp.com/api/v1/workspaces/get?token=..."},
                {"method": "GET", "url": "https://api.twistapp.com/api/v1/workspaces/getone?token=...&id=201"}]'
```

`POST /api/v1/batch`

Batching allows you to pass several requests in a single HTTP request. Once all operations have been completed, a consolidated response will be passed back to you and the HTTP connection will be closed.

> Return object

```json
[
  {
    "code": 200,
    "headers": "...",
    "body": "..."
  },
  {
    "code": 200,
    "headers": "...",
    "body": "..."
  }
]
```

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| requests | Array of Objects | Yes | The requests to send |
| requests["method"] | String | Yes | The HTTP method like `GET` or `POST` |
| requests["url"] | String | Yes | The completed URL with any arguments needed |

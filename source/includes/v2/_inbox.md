# Inbox

> Inbox object:

```json
[
   { 	"id" : 38677, ... },
   { 	"id" : 32038, ... },
   ...
]
```

The inbox unifies the start page view on all platforms. 

It is actually a list of thread objects. It doesn't contain all threads, but the
most recent threads ordered by date.


## Get inbox

> Example:

```shell
curl https://api.twistapp.com/api/v2/inbox/get \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -d workspace_id=5517
```

`GET /api/v2/inbox/get`

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| workspace_id *Integer* | Yes | The id of the workspace |
| limit *Integer* | No | Limits the number of threads returned, by default to `30` |
| newer_than_ts *Integer* | No | Limits threads to those newer whan the specified Unix time |
| older_than_ts *Integer* | No | Limits threads to those older whan the specified Unix time |

### Return value

A list of thread objects is returned.

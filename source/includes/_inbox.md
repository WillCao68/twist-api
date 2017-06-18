# Inbox
The inbox unifies the start page view on all platforms.


## Get inbox

`GET /api/v1/inbox/get`

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |
| limit | Number | No | Limits the number of threads returned, by default to `30` |
| newer_than_ts | Number | No | Limits threads to those newer whan the specified Unix time |
| older_than_ts | Number | No | Limits threads to those older whan the specified Unix time |

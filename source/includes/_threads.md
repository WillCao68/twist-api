# Threads

A thread is a discussion.


## Get thread

`GET /api/v1/threads/getone` 

Gets a thread object by id.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Get all threads

`GET /api/v1/threads/get`

Gets all threads in a channel.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| channel_id | Number | No | The id of the channel |
| workspace_id | Number | No | The id of the workspace |
| filter_by | String | No | A filter can be one of `attached_to_me`, `everyone` and `is_starred` |
| newer_than_ts | Number | No | Limits threads to those newer whan the specified Unix time |
| older_than_ts | Number | No | Limits threads to those older whan the specified Unix time |
| limit | Number | No | Limits the number of threads returned |
| as_ids | Boolean | No | If enabled, only the ids of the threads are returned |


## Add thread

`POST /api/v1/threads/add`

Adds a new thread to a channel.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| channel_id | Number | Yes | The id of the channel |
| title | String | Yes | The title of the new thread |
| content | String | Yes | The content of the new thread |
| attachments | Array of Objects | No | Files to attach to comment |
| recipients | Array of Numbers or String | No | The users that will participate in the thread, or `EVERYONE` |
| groups | Array of Numbers | No | The groups that will be notified |
| temp_id | Number | No | The temporary id of the thread |


## Update thread

`POST /api/v1/threads/update`

Updates an existing thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |
| title | String | No | The title of the thread |
| content | String | No | The content of the thread |
| attachments | Array of Objects | No | Files to attach to comment |


## Remove thread

`POST /api/v1/threads/remove`

Removes a thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Star thread

`POST /api/v1/threads/star`

Stars a thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Unstar thread

`POST /api/v1/threads/unstar`

Unstars a thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Move thread

`POST /api/v1/threads/move_to_channel`

Moves thread to a different channel.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |
| to_channel | Number | Yes | The target channel's id |


## Follow thread

`POST /api/v1/threads/follow`

Follows thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Unfollow thread

`POST /api/v1/threads/unfollow`

Unfollows thread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |


## Get unread threads

`GET /api/v1/threads/get_unread`

Gets unread threads in a workspace.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |


## Mark thread as read

`POST /api/v1/threads/mark_read`

Marks thread as read.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |
| obj_index | Number | Yes | The index of the last known read message |


## Mark thread as unread

`POST /api/v1/threads/mark_unread`

Marks thread as unread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the thread |
| obj_index | Number | Yes | The index of the last unread message |


## Mark all threads as read

`POST /api/v1/threads/mark_all_read`

Marks all thread in workspace or channel as read.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes, this or `channel_id` | The id of the workspace |
| channel_id | Number | Yes, this or `workspace_id` | The id of the channel |


## Clear unread threads

`POST /api/v1/threads/clear_unread`

Clears unread threads in workspace.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |

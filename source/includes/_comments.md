# Comments
A comment is a message in a thread.


## Get comment

`GET /api/v1/comments/getone`

Gets a single comment object by id.

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the comment |


## Get all comments

`GET /api/v1/comments/get`

Gets all comments in a channel.

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| thread_id | Number | No | The id of the thread |
| newer_than_ts | String | No | Limit comments to those newer than the specified Unix timestamp |
| older_than_ts | String | No | Limit comments to those older than the specified Unix timestamp |
| from_obj_index | Number | No | Limit comments starting at the specified object index |
| to_obj_index | String | No | Limit comments ending at the specified object index |
| limit | Number | No | Limits the number of comments returned, by default `20` |
| order_by | String | No | The order of the comments returned one of `DESC` or `ASC` |
| as_ids | Boolean | No | If enabled, only the ids of the comments are returned |


## Add comment

`POST /api/v1/comments/add`

Adds a new comment to a thread.

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| thread_id | Number | Yes | The id of the thread |
| content | String | Yes | The content of the new comment |
| attachments | Array of Objects | No | Files to attach to comment |
| recipients | Array of Numbers or String | No | The users that will be notified, or `EVERYONE` or `EVERYONE_IN_THREAD` |
| groups | Array of Numbers | No | The groups that will be notified |
| temp_id | Number | No | The temporary id of the comment |
| mark_thread_position | Boolean | No | By default, the position of the thread is marked |


## Update comment

`POST /api/v1/comments/update`

Updates an existing comment.

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the comment |
| content | String | No | The content of the comment |
| attachments | Array of Objects | No | Files to attach to comment |


## Remove comment

`POST /api/v1/comments/remove`

Removes a comment \(only user's own comments can be removed\).

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the comment |


## Mark position

`POST /api/v1/comments/mark_position`

Marks the position of a thread.

#### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| thread_id | Number | Yes | The id of the thread |
| comment_id | Number | Yes | The id of the comment |


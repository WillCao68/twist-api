# Reactions

Reactions can be added to threads, comments or conversation messages.


## Get reactions

`POST /api/v1/reactions/get`

Gets reactions of a thread, comment or conversation message.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| thread_id | Number | Yes, this or `comment_id` or `message_id` | The id of the thread |
| comment_id | Number | Yes, this or `thread_id` or `message_id` | The id of the comment |
| message_id | Number | Yes, this or `thread_id` or `comment_id` | The id of the conversation message |


## Add a reaction

`POST /api/v1/reactions/add`

Adds a reaction to a thread, comment or conversation message.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| reaction | String | Yes | The reaction to add |
| thread_id | Number | Yes, this or `comment_id` or `message_id` | The id of the thread |
| comment_id | Number | Yes, this or `thread_id` or `message_id` | The id of the comment |
| message_id | Number | Yes, this or `thread_id` or `comment_id` | The id of the conversation message |


## Remove a reaction

`POST /api/v1/reactions/remove`

Removes a reaction from thread, comment or conversation message.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| reaction | String | Yes | The reaction to remove |
| thread_id | Number | Yes, this or `comment_id` or `message_id` | The id of the thread |
| comment_id | Number | Yes, this or `thread_id` or `message_id` | The id of the comment |
| message_id | Number | Yes, this or `thread_id` or `comment_id` | The id of the conversation message |


# Conversations
A conversation is a direct message exchange between one or more users.


## Get conversation

`GET /api/v1/conversations/getone`

Gets a single conversation object.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |


## Get all conversations

`GET /api/v1/conversations/get`

Gets all conversations of a user in a workspace.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |
| limit | Number | No | Limits the number of conversations |
| newer_than_ts | Number | No | Limits conversations to those newer whan the specified Unix time |
| older_than_ts | Number | No | Limits conversations to those older whan the specified Unix time |
| order_by | String | No | The order of the comments returned one of `DESC` or `ASC` |
| archived | Boolean | No | If enabled, only archived converations are returned. By default it's off. |


## Get or create conversation

`POST /api/v1/conversations/get_or_create`

Gets or creates a conversation with one or more users.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |
| user_ids | Array of Numbers | Yes | The users that will participate in the conversation |


## Update conversation

`POST /api/v1/conversations/update`

Updates an existing conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| title | String | Yes | The title of the conversation |
| archived | Boolean | No | If enabled, the conversation is marked as archived |


## Add user

`POST /api/v1/conversations/add_user`

Adds a person to a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| user_id | Number | Yes | The user's id |


## Add users

`POST /api/v1/conversations/add_users`

Adds several persons to a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| user_ids | Array of Numbers | Yes | The ids of the users |


## Remove user

`GET /api/v1/conversations/remove_user`

Removes a person from a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| user_id | Number | Yes | The user's id |


## Remove users

`GET /api/v1/conversations/remove_users`

Removes several persons from a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| user_ids | Array of Numbers | Yes | The ids of the users |


## Archive conversation

`POST /api/v1/conversations/archive`

Archives a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |


## Unarchive conversation

`POST /api/v1/conversations/unarchive`

Unarchives a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |


## Get unread conversations

`GET /api/v1/conversations/get_unread`

Gets unread conversations.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |


## Mark conversation as read

`POST /api/v1/conversations/mark_read`

Marks a conversation as read.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| conversation_id | Number | Yes | The id of the conversation |
| message_id | Number | Yes | The id of the message, which must be the last message in the conversation |


## Mark conversation as unread

`POST /api/v1/conversations/mark_unread`

Marks a conversation as unread.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| conversation_id | Number | Yes | The id of the conversation |
| message_id | Number | Yes | The id of the message, which will indicate the position |


## Mute conversation

`POST /api/v1/conversations/mute`

Mutes a conversation for a number of minutes.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |
| minutes | Number | Yes | The number of minutes to mute the conversation |


## Unmute conversation

`POST /api/v1/conversations/unmute`

Unmutes a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation |


## Get conversation message

`GET /api/v1/conversation_messages/getone`

Gets a single conversation message.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the conversation message |


## Get all conversation messages

`GET /api/v1/conversation_messages/get`

Gets messages from a conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| conversation_id | Number | Yes | The id of the conversation |
| limit | Number | No | Limits the number of messages returned |
| from_obj_index | Number | No | Limit messages starting at the specified object index |
| to_obj_index | String | No | Limit messages ending at the specified object index |
| order_by | String | No | The order of the conversations returned one of `DESC` or `ASC` |
| as_ids | Boolean | No | If enabled, only the ids of the messages are returned |


## Add message to conversation

`POST /api/v1/conversation_messages/add`

Adds a message to an existing conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| conversation_id | Number | Yes | The id of the conversation |
| content | String | Yes | The content of the new message |
| attachments | String | No | Attachments to the new message |


## Update message in conversation

`POST /api/v1/conversation_messages/update`

Updates a message in conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the message |
| content | String | No | The content of the new message |
| attachments | String | No | Attachments to the new message |


## Remove message from conversation

`POST /api/v1/conversation_messages/remove`

Removes a message from conversation.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| id | Number | Yes | The id of the message |

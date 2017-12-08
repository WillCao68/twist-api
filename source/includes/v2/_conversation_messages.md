# Conversation messages

A conversation message is a message between one or more users participating in a
conversation.

> Conversation message object:

```json
{
   "id" : 514069,
   "content" : "Hi!",
   "creator" : 10073,
   "conversation_id" : 13037,
   "workspace_id" : 5517
   "obj_index" : 0,
   "attachments" : [],
   "actions" : [],
   "reactions" : {},
   "is_deleted" : false,
   "system_message" : null,
   "posted_ts" : 1497970956,
},
```

### Properties of conversation message object

| Name | Description |
| ---- | --- |
| id *Integer* | The id of the message |
| content *String* | The content of the message |
| creator *Integer* | The user that added the message |
| conversation_id *Integer* | The id of the conversation |
| workspace_id *Integer* | The id of the workspace |
| obj_index *Integer* | The index of the message in regards to all other messages in the conversation |
| attachments *List of [Attachments](#attachments)* | Files attached to the comment |
| actions *List of [Action buttons](#action-buttons)* | Action buttons attached to the comment |
| reactions *Object* | Reactions to the thread, where keys are the reactions and values the users that had that reaction |
| is_deleted *Integer* | Whether the message is deleted |
| system_message *String* | A system message |
| posted_ts *Integer* | The Unix time when the message was created |


## Get message

> Example:

```shell
curl --get https://api.twistapp.com/api/v2/conversation_messages/getone \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=514069
```

`GET /api/v2/conversation_messages/getone`

Gets a single conversation message.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the conversation message |

### Return value

A conversation message object is returned.


## Get all messages

> Example:

```shell
curl --get https://api.twistapp.com/api/v2/conversation_messages/get \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d conversation_id=13037
```

`GET /api/v2/conversation_messages/get`

Gets messages from a conversation.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| conversation_id *Integer* | Yes | The id of the conversation |
| limit *Integer* | No | Limits the number of messages returned |
| from_obj_index *Integer* | No | Limit messages starting at the specified object index |
| to_obj_index *String* | No | Limit messages ending at the specified object index |
| order_by *String* | No | The order of the conversations returned one of `DESC` or `ASC` |
| as_ids *Boolean* | No | If enabled, only the ids of the messages are returned |

### Return value

A list of conversation message objects is returned.


## Add message to conversation

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/conversation_messages/add \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d conversation_id=13037 \
  -d content="Hello!"

# Create a message with an attachment using two requests
curl -X POST https://api.twistapp.com/api/v2/conversation_messages/add \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d conversation_id=13037 \
  -d content="Hello!" \
  -d attachments=[$(curl -X POST https://api.twistapp.com/api/v2/attachments/upload -F attachment_id=$(uuidgen) -F file_name=@mytext.txt -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf")]
```

`POST /api/v2/conversation_messages/add`

Adds a message to an existing conversation.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| conversation_id *Integer* | Yes | The id of the conversation |
| content *String* | Yes | The content of the new message |
| attachments *List of [Attachments](#attachments)* | No | List of attachments to the message. It must follow the JSON format returned by [attachment#upload](#upload-an-attachment) |
| actions *List of [Action Buttons](#action-buttons)* | No | List of action to the new message. More information about the format of the object available at the [add an action button submenu](#add-an-action-button) |


### Return value

A conversation message object is returned.


## Update message in conversation

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/conversation_messages/update \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d conversation_id=13037 \
  -d content="Hello!"

# Update a message with an attachment using two requests
curl -X POST https://api.twistapp.com/api/v2/conversation_messages/update \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=130371 \
  -d content="Hello!" \
  -d attachments=[$(curl -X POST https://api.twistapp.com/api/v2/attachments/upload -F attachment_id=$(uuidgen) -F file_name=@mytext.txt -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf")]
```

`POST /api/v2/conversation_messages/update`

Updates a message in conversation.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the message |
| content *String* | No | The content of the new message |
| attachments *List of [Attachments](#attachments)* | No | List of attachments to the message. It must follow the JSON format returned by [attachment#upload](#upload-an-attachment) |
| actions *List of [Action Buttons](#action-buttons)* | No | List of action to the message. More information about the format of the object available at the [add an action button submenu](#add-an-action-button) |

### Return value

A conversation message object is returned.


## Remove message from conversation

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/conversation_messages/remove \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=514069
```

`POST /api/v2/conversation_messages/remove`

Removes a message from conversation.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the message |

> Return value:

```json
{
   "status": "ok"
}
```

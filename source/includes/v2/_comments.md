# Comments

A comment is a message in a thread.

> Comment object:

```json
{
   "id" : 206113,
   "content" : "OK!",
   "creator" : 10076,
   "thread_id" : 32038,
   "channel_id" : 6984,
   "workspace_id" : 5517
   "obj_index" : 2,
   "attachments" : [],
   "recipients" : [
      10073
   ],
   "groups" : [],
   "reactions" : {
      "👍" : [
         10076
      ]
   },
   "is_deleted" : false,
   "system_message" : null,
   "posted_ts" : 1494489787,
}
```

### Properties of comment object

| Name | Description |
| ---- | --- |
| id *Integer* | The id of the comment |
| content *String* | The content of the new comment |
| creator *Integer* | The user that added the comment |
| thread_id *Integer* | The id of the thread |
| channel_id *Integer* | The id of the channel |
| workspace_id *Integer* | The id of the workspace |
| attachments *List of [Attachments](#attachments)* | Files attached to the comment |
| actions *List of [Action buttons](#action-buttons)* | Action buttons attached to the comment |
| recipients *List of Integers or String* | The users that will be notified, or `EVERYONE` or `EVERYONE_IN_THREAD` |
| groups *List of Integers* | The groups that will be notified |
| reactions *Object* | Reactions to the thread, where keys are the reactions and values the users that had that reaction |
| is_deleted *Integer* | Whether the thread is deleted |
| system_message *String* | A system message |
| posted_ts *Integer* | The Unix time when the thread was created |


## Get comment

> Example:

```shell
curl --get https://api.twistapp.com/api/v2/comments/getone \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=206113
```

`GET /api/v2/comments/getone`

Gets a single comment object by id.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the comment |

### Return value

A comment object is returned.


## Get all comments

> Example:

```shell
curl --get https://api.twistapp.com/api/v2/comments/get \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d thread_id=32038
```

`GET /api/v2/comments/get`

Gets all comments in a thread.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| thread_id *Integer* | Yes | The id of the thread |
| newer_than_ts *String* | No | Limit comments to those newer than the specified Unix timestamp |
| older_than_ts *String* | No | Limit comments to those older than the specified Unix timestamp |
| from_obj_index *Integer* | No | Limit comments starting at the specified object index |
| to_obj_index *String* | No | Limit comments ending at the specified object index |
| limit *Integer* | No | Limits the number of comments returned, by default `20` |
| order_by *String* | No | The order of the comments returned one of `DESC` or `ASC` |
| as_ids *Boolean* | No | If enabled, only the ids of the comments are returned |

### Return value

A list of comment objects is returned.


## Add comment

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/comments/add \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d thread_id=32038 \
  -d content="OK!"

# Create a comment with an attachment using two requests
curl -X POST https://api.twistapp.com/api/v2/comments/add \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d thread_id=32038 \
  -d content="OK!" \
  -d attachments=[$(curl -X POST https://api.twistapp.com/api/v2/attachments/upload -F attachment_id=$(uuidgen) -F file_name=@mytext.txt -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf")]
```

`POST /api/v2/comments/add`

Adds a new comment to a thread.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| thread_id *Integer* | Yes | The id of the thread |
| content *String* | Yes | The content of the new comment |
| attachments *List of [Attachments](#attachments)* | No | List of attachments to the new comment. It must follow the JSON format returned by [attachment#upload](#upload-an-attachment) |
| actions *List of [Action Buttons](#action-buttons)* | No | List of action to the new comment. More information about the format of the object available at the [add an action button submenu](#add-an-action-button) |
| recipients *List of Integers or String* | No | The users that will be notified, or `EVERYONE` or `EVERYONE_IN_THREAD` |
| groups *List of Integers* | No | The groups that will be notified |
| temp_id *Integer* | No | The temporary id of the comment |
| mark_thread_position *Boolean* | No | By default, the position of the thread is marked |
| send_as_integration *Boolean* | No | Displays the integration as the comment creator |

### Return value

A comment object is returned.


## Update comment

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/comments/update \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=206113 \
  -d content="OK!"

# Update a comment with an attachment using two requests
curl -X POST https://api.twistapp.com/api/v2/comments/update \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=206113 \
  -d content="OK!" \
  -d attachments=[$(curl -X POST https://api.twistapp.com/api/v2/attachments/upload -F attachment_id=$(uuidgen) -F file_name=@mytext.txt -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf"])
```

`POST /api/v2/comments/update`

Updates an existing comment.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the comment |
| content *String* | No | The content of the comment |
| attachments *List of [Attachments](#attachments)* | No | List of attachments to the new comment. It must follow the JSON format returned by [attachment#upload](#upload-an-attachment) |
| actions *List of [Action Buttons](#action-buttons)* | No | List of action to the new comment. More information about the format of the object available at the [add an action button submenu](#add-an-action-button) |


### Return value

A comment object is returned.


## Remove comment

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/comments/remove \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d id=206113
```

`POST /api/v2/comments/remove`

Removes a comment \(only user's own comments can be removed\).

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| id *Integer* | Yes | The id of the comment |

> Return value:

```json
{
   "status": "ok"
}
```

## Mark position

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/comments/mark_position \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d thread_id=32038 \
  -d comment_id=206113
```

`POST /api/v2/comments/mark_position`

Marks the position of a thread.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| thread_id *Integer* | Yes | The id of the thread |
| comment_id *Integer* | Yes | The id of the comment |

> Return value:

```json
{
   "status": "ok"
}
```

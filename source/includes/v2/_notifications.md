# Notifications

The user's last notifications.

> Notification object:

```json
{
   "notifications" : [
      {
         "id" : 1,
         "type_id" : 1,
         "workspace_id" : 5517,
         "channel_id" : 6984,
         "thread_id" : 32038,
         "comment_id" : 206113
         "by_user_id" : 10076,
         "posted_ts" : 1494489787,
      }
   ],
   "last_read" : 0
}
```

### Properties of notification object

| Name | Description |
| ---  | ----------- |
| id *Integer* | The id of the notification. |
| type_id *Integer* | The notification type: `1` when added to a comment, `2` when added to a thread, `3` when added to a workspace, `4` when removed from a workspace, `5` when added to a channel, and `6` when removed from a channel. |
| workspace_id *Integer* | The id of the workspace. |
| channel_id *Integer* | The id of the channel. |
| thread_id *Integer* | The id of the thread. |
| comment_id *Integer* | The id of the comment. |
| by_user_id *Integer* | The id of the user that triggered the notification (notified the receiving user). |
| posted_ts *Integer* | The Unix time when the notification took place. |
| last_read *Integer* | The id of the last read notification. |


## Get last notifications

> Example:

```shell
curl https://twistapp.com/api/v2/notifications/get \
    -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf"
```

`GET /api/v2/notifications/get`

Gets the last notifications of the user.

### Parameters

| Name | Required | Description |
| ---- | -------- | ----------- |
| limit *Integer* | No | Limits the number of threads returned. |


### Return value

A list of notification objects is returned.


## Mark notifications as read

> Example:

```shell
curl -X POST https://twistapp.com/api/v2/notifications/mark_read \
    -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf"
    -d notification_id=1
```

`POST /api/v2/notifications/mark_read`

Marks everything after specified notification as read.

### Parameters

| Name | Required | Description |
| ---- | ---- | -------- | ----------- |
| notification_id *Integer* | Yes | The last read notification id. |

> Return value:

```json
{
   "status": "ok"
}
```

## Reset notifications

> Example:

```shell
curl -X POST https://twistapp.com/api/v2/notifications/reset \
    -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf"
```

`POST /api/v2/notifications/reset`

Resets all notifications read status.

> Return value:

```json
{
   "status": "ok"
}
```

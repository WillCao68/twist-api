# Notifications settings

The user's notification settings allow to setup email and push settings.

> Notifications settings object:

```json
{
   "desktop_added_to_ws" : true,
   "desktop_comments" : false,
   "desktop_conversations" : true,
   "desktop_removed_from_ws" : true,
   "desktop_threads" : false,
   "email_added_to_ws" : true,
   "email_aggregate" : true,
   "email_comments" : true,
   "email_conversations" : true,
   "email_removed_from_ws" : true,
   "email_threads" : true,
   "push_added_to_ws" : true,
   "push_comments" : false,
   "push_conversations" : true,
   "push_delay" : 120,
   "push_removed_from_ws" : true,
   "push_threads" : false,
   "badge_conversations" : true,
   "badge_threads" : true,
}
```

### Properties of notifications settings object

| Name | Description |
| ---- | --- |
| desktop_conversations *Boolean* | Desktop notifications for new messages on conversations |
| desktop_comments *Boolean* | Desktop notifications for new comments attached to user |
| desktop_threads *Boolean* | Desktop notifications for new threads attached to user |
| desktop_added_to_ws *Boolean* | Desktop notifications when added to workspaces |
| desktop_removed_from_ws *Boolean* | Desktop notifications when removed from workspaces |
| email_conversations *Boolean* | Email notifications for new messages on conversations |
| email_comments *Boolean* | Email notifications for new comments attached to user |
| email_threads *Boolean* | Email notifications for new threads attached to user |
| email_added_to_ws *Boolean* | Email notifications when added to workspaces |
| email_removed_from_ws *Boolean* | Email notifications when removed from workspaces |
| email_aggregate *Boolean* | Email notifications digest |
| push_conversations *Boolean* | Push notifications for new messages on conversations |
| push_comments *Boolean* | Push notifications for new comments attached to user |
| push_delay *Integer* | Number of seconds before sending a push notification |
| push_threads *Boolean* | Push notifications for new threads attached to user |
| push_added_to_ws *Boolean* | Push notifications when added to workspaces |
| push_removed_from_ws *Boolean* | Push notifications when removed from workspaces |
| badge_threads *Boolean* | Badge notifications on unread threads (iOS) |
| badge_conversations *Boolean* | Badge notifications on unread conversations (iOS) |


## Get notification settings

> Example:

```shell
curl https://api.twistapp.com/api/v2/notifications_settings/v2/get \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -d workspace_id=5517
```

`GET /api/v2/notifications_settings/v2/get`

Gets the user's current notification settings.

### Parameters

| Name | Required | Description |
| ---- | -------- | ----------- |
| workspace_id *Integer | Yes | The workspace id |

### Return value

A notifications settings object is returned.


## Update notifications settings

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/notifications_settings/v2/update \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -d workspace_id=5517 \
  -d setting=desktop_conversations \
  -d value=true
```

`POST /api/v2/notifications_settings/v2/update`

> Return value:

```json
{
   "status": "ok"
}
```

Updates user notifications settings.

### Parameters

| Name | Required | Description |
| ---- | -------- | ----------- |
| workspace_id *Integer | Yes | The workspace id |
| setting *String* | Yes | The name of the notifications setting to update, see above |
| value *Boolean* | Yes | The value of the notifications setting to update |


## Update many notifications settings

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/notifications_settings/v2/update_many \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -d workspace_id=5517
  -d mapping='{"desktop_conversations":true,"email_comments":false}'
```

`POST /api/v2/notifications_settings/v2/update_many`

> Return value:

```json
{
   "status": "ok"
}
```

Updates multiple user notifications settings at once.

### Parameters

| Name | Required | Description |
| ---- | -------- | ----------- |
| workspace_id *Integer | Yes | The workspace id |
| mapping *Object* | Yes | The notifications settings to update |

# Loop In

This allows to add threads to a channel, add comments to a thread, or messages
to conversation by sending them to an email address.

## Get or create a loop in email

`POST /api/v1/loop_in/get_or_create`

Gets or creates a loop in email.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| obj_type | String | Yes | The type of the object, one of `CHANNEL`, `THREAD` or `CONVERSATION` |
| obj_id | Number | Yes | The id of the object |


## Disable loop in email

`POST /api/v1/loop_in/disable`

Disables a loop in email.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| obj_type | String | Yes | The type of the object, one of `CHANNEL`, `THREAD` or `CONVERSATION` |
| obj_id | Number | Yes | The id of the object |


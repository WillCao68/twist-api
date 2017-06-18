# URL Join

This allows one to join a workspace using a special URL invite link.


## Get or create URL join link

`POST /api/v1/url_join/get_or_create`

Gets or creates a URL join link to a workspace.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |


## Disable URL join link

`POST /api/v1/url_join/disable`

Disables a URL join link to a workspace.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| workspace_id | Number | Yes | The id of the workspace |


## Join workspace

`POST /api/v1/url_join/join_workspace`

Joins user to invited workspace using the URL link.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| url_invite_code | Number | Yes | The URL join link |


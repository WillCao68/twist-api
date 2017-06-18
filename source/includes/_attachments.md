# Attachments

Files can be attached to threads, comments, or conversation messages.

### Properties
| Name | Type | Description |
| --- | --- | --- | --- |
| attachment_id | String | The id of the attachment |
| title | String | The title of the attachment |
| url | String | The URL where the file is located |
| url_type | String | The type of the file, such as `file` or `image` |
| file_name | String | The file's name |
| file_size | Number | The file's size in bytes |
| underlying_type | String | The file's media or content type (MIME)|
| description | String | The description of the attachment |
| image  | String | If file is an image, the URL to the image file |
| image_width | Number | If file is an image, the width of the image |
| image_height | Number | If file is an image, the height of the image |
| duration | String | If file is audio, the duration of the audio |
| upload_state | String | Upload state is `uploaded` on success, or `failed` otherwise |


## Upload an attachment

`POST /api/v1/attachments/upload`

Uploads a file.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| file_name | String | Yes | The name of the file to be uploaded |


## Remove an attachment

`POST /api/v1/attachments/remove`

Removes attachment from thread, comment or conversation message.

### Parameters
| Name | Type | Required | Description |
| --- | --- | --- | --- |
| attachment_id | Number | Yes | The id of the attachment |
| thread_id | Number | Yes, this or `comment_id` or `message_id` | The id of the thread |
| comment | Number | Yes, this or `thread_id` or `message_id` | The id of the comment |
| message_id | Number | Yes, this or `thread_id` or `comment_id` | The id of the conversation message |

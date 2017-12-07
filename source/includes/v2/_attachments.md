# Attachments

Files can be attached to threads, comments, or conversation messages.

**Note:** the maximum allowed size for the attachment is 100MB

> Example:

```json
{
   "attachment_id" : "c8f962d3-491b-4a43-92c2-43f7ac076408",
   "title" : "image.png",
   "url" : "https://xxx.cloudfront.net/xxx/as/image.png",
   "url_type" : "image",
   "file_name" : "image.png",
   "file_size" : 21601,
   "underlying_type" : "image/png",
   "image" : "https://xxx.cloudfront.net/xxx/as/image.png",
   "image_height" : 100,
   "image_width" : 100,
   "upload_state" : "uploaded"
}
```


### Properties

| Name | Description |
| --- | --- |
| attachment_id *String* | The id of the attachment |
| title *String* | The title of the attachment |
| url *String* | The URL where the file is located |
| file_name *String* | The file's name |
| file_size *Integer* | The file's size in bytes |
| underlying_type *String* | The file's media or content type (MIME)|
| upload_state *String* | Upload state is `uploaded` on success, or `failed` otherwise |
| url_type *String* | The type of the file, such as `file` or `image` |
| image *String* | If file is an `image`, the URL to the image file |
| image_width *Integer* | If file is an `image`, the width of the image |
| image_height *Integer* | If file is an `image`, the height of the image |
| duration *String* | If file is `audio`, the duration of the audio |


## Upload an attachment

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/attachments/upload \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -F attachment_id=c8f962d3-491b-4a43-92c2-43f7ac076408 \
  -F file_name=@image.png
```

`POST /api/v2/attachments/upload`

Uploads a file.

### Parameters

| Name | Required | Description |
| --- | --- | --- |
| attachment_id *String* | Yes | A UUID that will be the id of the attachment |
| file_name *String* | Yes | The name of the file to be uploaded |

### Return value

An attachment object is returned.


## Remove an attachment

> Example:

```shell
curl -X POST https://api.twistapp.com/api/v2/attachments/upload \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \ 
  -d attachment_id=c8f962d3-491b-4a43-92c2-43f7ac076408 \
  -d comment_id=241432
```

`POST /api/v2/attachments/remove`

Removes attachment from thread, comment or conversation message.

### Parameters
| Name | Required | Description |
| --- | --- | --- |
| attachment_id *Integer* | Yes | The id of the attachment |
| thread_id *Integer* | Yes, this or `comment_id` or `message_id` | The id of the thread |
| comment_id *Integer* | Yes, this or `thread_id` or `message_id` | The id of the comment |
| message_id *Integer* | Yes, this or `thread_id` or `comment_id` | The id of the conversation message |

> Return value:

```json
{
   "status": "ok"
}
```

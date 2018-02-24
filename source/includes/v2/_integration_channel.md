# &#8627; Channel

Channel integrations are installed on a channel level and can post new threads.

It provides an URL for distribution and installation, so the integration
developer can provide it to his users. The installation page asks for write
permission to one channel and also which teams it should notify. In case the
schedule option was used, it will also ask for the recurrence period and source
of data.

**Example usage**: A growth report that Twist posts on a weekly or monthly
basis to the same channel


## Incoming webhook

Sometimes a developer just wants an **incoming webhook** URL to post
via manually via `curl` (for example) or to include in the Continuous
Integration build. It can be done via [OAuth integration](#oauth) by
using the token provided or via channel or thread integration.

To do that using a channel integration, you just have to create and install
it. After the installation, Twist will provide the URL for manual posting.

Please follow the subsection on
[How to post data from a channel integration](#how-to-post-data-from-a-channel-integration).


## Outgoing webhook

**Note**: Outgoing webhook for channels is really different from [the
one provided by OAuth](#outgoing-webhook). 😉

Outgoing webhooks send data when an activity happens (e.g. a new
comment is added to the thread or an uninstall happens).

Its sends an HTTPS POST request to your specified URL and your webhook
handler can respond to add data back to Twist. The payload depends on
the integration type.

The outgoing hooks can work with any language or framework — as long as they
support HTTPS and JSON.


### POST Parameters when users add new objects

When a new message, thread or a new comment is added, you can expect following
parameters.

| Name | Optional | Description |
| --- | --- | --- |
| event_type *String* | No | Can be `message`, `thread` or `comment` — depending where the slash command was used |
| workspace_id *Integer* | No | The workspace the object was posted in |
| content *String* | No | The content of object, e.g. thread or message content |
| user_id *Integer* | No | The id of the poster |
| user_name *String* | No | The name of the poster |
| conversation_id *Integer* | Yes | Will be set if `event_type` is `message` |
| conversation_title *String* | Yes | Will be set if `event_type` is `message` |
| thread_id *Integer* | Yes | Will be set if `event_type` is `thread` or `comment` |
| thread_title *String* | Yes | Will be set if `event_type` is `thread` or `comment` |
| channel_id *Integer* | Yes | Will be set if `event_type` is `thread` or `comment` |
| comment_id *Integer* | Yes | Will be set if `event_type` is `comment` |
| command *String* | Yes | If the integration type is a slash command we'll include the command, e.g. `/hello` |
| command_argument *String* | Yes | If the integration type is a slash command we'll include the command argument, e.g. for `/hello world` it would be `world` |


### POST Parameters when an uninstall happens

When a team uninstalls your integration, you can expect following
parameters. You can use this to clean up any state you may have on your end.

| Name | Optional | Description |
| --- | --- | --- |
| event_type *String* | No | Will be `uninstall` |
| install_id *Integer* | No | The unique id of the installation |
| workspace_id *Integer* | No | The workspace the installation belonged to |
| user_id *Integer* | No | The id of the uninstaller |
| user_name *String* | No | The full name of the uninstaller |


### POST Parameters when a ping happens

For debugging purposes, you might get a `ping` payload. You should respond back
with a JSON `{"content": "pong"}`.

| Name | Optional | Description |
| --- | --- | --- |
| event_type *String* | No | Will be `ping` |
| user_id *Integer* | No | The id of the pinger |
| user_name *String* | No | The full name of the pinger |


### Adding content back

If your handler wishes to post a response back, use the following JSON
response:

`{"content": "42 is the answer to everything."}`


### Error handling

Non-200 responses will be retried 10 times in the span of 12 hours.


## Configure URL

We redirect users to the configure URL when setting up the integration. The
configured URL lets you connect the installation to your app and also
includes [an incoming webhook](#channel-incoming-webhook) URL, which you can use
as an easy way to manually post new threads into Twist as an integration.

You'll get following GET parameters served to your configure URL:


### GET Parameters

| Name | Required | Description |
| --- | --- | --- |
| install_id *Integer* | Yes | The unique id of the installation |
| post_data_url *String* | Yes | A unique URL you can use to post content to Twist |
| user_id *Integer* | Yes | The id of the installer |
| user_name *String* | Yes | The full name of the installer |

To get back to the installation page, please use
`https://twistapp.com/integrations/installation/{install_id}`.

## How to post data from a channel integration

> CURL example

```shell
curl -X POST -H 'Content-type: application/json' \
    --data '{"content":"42?"}' \
    "https://hooks.twistapp.com/api/v2/integration_incoming/post_data?install_id=...&install_token=..."
```

Simply make a POST request to the `post_data_url`. In the POST include your data
encoded in JSON.

### POST Parameters

| Name | Required | Description |
| --- | --- | --- |
| content *String* | Yes | The content of the new object |
| title *String* | No | Title of the new thread |


## URL Reports

This feature provides a way to retrieve real content from an external source via
GET request. When combined with the `schedule` feature may become a way to
provide periodic information with real data.

### Returning Markdown content

Automatic URL Reports can return plain Markdown content and Twist will use it as
content for the new thread.

For example, the URL can return following (e.g. to generate automatic growth
reports):

```text
Apple today announced financial results for its fiscal 2017 second quarter ended April 1, 2017.

Core numbers:

* $78.4 Billion Revenue
* 78.3 Million iPhones
* 13.1 Million iPads Sold
* ...
```

### Returning JSON content

The URL content can also return a JSON object specifying `title` and `content`
of the new thread.


```json
Content-type: application/json
{
    "title": "Webdev snippets | <date>",
    "content": "Please share your weeky snippets"
}
```

Note that you can use `<date>` in the `title`, and we will convert it to the
current date.


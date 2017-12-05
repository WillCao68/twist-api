# &#8627; Channel

Channel integrations are installed on a channel level and can post new threads.

It provides an URL for distribution and installation, so the integration
developer can provide it to his users. The installation page asks for write
permission to one channel and also which teams it should notify. In case the
schedule option was used, it will also ask for the recurrence period and source
of data.

**Example usage**: A growth report that Twist posts on a weekly or monthly
basis to the same channel


## Channel Incoming webhook

Sometimes a developer just want an **incoming webhook** URL to post via some script
or external system without setting up a webserver and so on. It can be done
via [OAuth integration](#oauth) by using the token provided or via channel or
thread integration.

To do that using a channel integration, you just have to create and install
it. After the installation, Twist will provide the URL for manual posting.

Please follow the subsection on
[How to post data from a channel integration](#how-to-post-data-from-a-channel-integration).


## Configure URL

We redirect users to the configure URL when setting up the integration. The
configured URL lets you connect the installation with your app and also
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
    https://hooks.twistapp.com/...
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


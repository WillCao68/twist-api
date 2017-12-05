# &#8627; Thread

Thread integrations are installed on a thread level, and they can post new
comments.

It provides an URL for distribution and installation, so the
integration developer can provide it to his users. The installation
page asks for write permission to one channel or thread and which
teams it should notify.

**Example usage**: Post comments when new issues are added to a Github
repository.


## Thread Incoming webhook

Sometimes a developer just want **an incoming webhook** URL to post via
some script or external system without setting up a webserver and so
on. It can be done via [OAuth integration](#oauth) by using the token
provided or via channel or thread integration.

To do that using a thread integration, you just have to create and
install it. After the installation, Twist will provide the URL for
manual posting.

Please follow the subsection on
[How to post data from a thread integration](#how-to-post-data-from-a-thread-integration).


## Configure URL

We redirect users to the configure URL when setting up the
integration. The configured URL lets you connect the installation with
your app and also
includes [an incoming webhook](#thread-incoming-webhook) URL, which
you can use as an easy way to post messages into Twist.

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

## How to post data from a thread integration

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

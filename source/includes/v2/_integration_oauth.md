# &#8627; OAuth

The OAuth integration is the most powerful way to use the Twist API
but it's also the one that needs a more work for a full setup. The
steps needed to setup are described in our [OAuth2](#oauth2) section.

**Example usage**: Integrate an application with Twist, creating new
workspaces, channels, threads, and/or messages.

## Retrieving a token

Sometimes a developer just wants a **token** so he/she can use all the
endpoints of the API for personal purposes or create a proof of
concept. For these cases, when the OAuth integration is created we
provide a **test token**.

The test token is a result of the [OAuth2](#oauth2) process for the
current logged user and will have the full scope access. 

```shell
curl -X POST https://api.twistapp.com/api/v2/your_endpoint \
  -H "Authorization: Bearer Gen3rated_t3st_t0k3n" \
```

The generated token can be used in the authorization header to make
requests to all endpoints in the API.


## Outgoing webhook

Outgoing webhooks for OAuth integrations are based on [REST
hooks](http://resthooks.org/), so they are different from
[channels](##outgoing-webhook151) and
[threads](#outgoing-webhook157).

The webhooks for the OAuth integration provide fine-grained access to
the event hooks. It's possible to subscribe and unsubscribe to any
available event programmatically.

These are the supported events:

| Event type | Description |
| ---------- | ----------- |
| workspace_added | Triggers when a workspace is added |
| workspace_updated | Triggers when a workspace is updated |
| workspace_deleted | Triggers when a workspace is deleted |
| workspace_user_added | Triggers when a user is added to a workspace |
| workspace_user_updated | Triggers when a user is updated inside a workspace |
| workspace_user_removed | Triggers when a user is removed from a workspace |
| channel_added | Triggers when a channel is added |
| channel_updated | Triggers when a channel is updated |
| channel_deleted | Triggers when a channel is deleted |
| channel_user_added | Triggers when a user is added to a channel |
| channel_user_updated | Triggers when a user is updated inside a channel |
| channel_user_removed | Triggers when a user is removed from a channel |
| thread_added | Triggers when a thread is added |
| thread_updated | Triggers when a thread is updated |
| thread_deleted | Triggers when a thread is deleted |
| comment_added | Triggers when a comment is added |
| comment_updated | Triggers when a comment is updated |
| comment_deleted | Triggers when a comment is deleted |
| message_added | Triggers when a message is added |
| message_updated | Triggers when a message is updated |
| message_deleted | Triggers when a message is deleted |
| group_added | Triggers when a group is added |
| group_updated | Triggers when a group is updated |
| group_deleted | Triggers when a group is deleted |
| group_user_added | Triggers when a user is added to a group |
| group_user_removed | Triggers when a user is removed from a group |


### Subscribe to a hook

> Example

```shell
curl https://api.twistapp.com/api/v2/hooks/subscribe \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d target_url=https://hooks.yourdomain.com/<unique_target_url> \
  -d event=workspace_user_added
```

To start listening to changes you have to subscribe to a hook. The
following parameters are accepted in the subscribe request:

| Name | Required | Description |
| --- | --- | --- |
| target_url *String* | Yes | The URL we should call when an event happens |
| event_type *String* | Yes | What Twist event should trigger the call |
| workspace_id *Integer* | No | Only trigger for following `workspace_id` |
| channel_id *Integer* | No | Only trigger for following `channel_id` |
| thread_id *Integer* | No | Only trigger for following `thread_id` |
| conversation_id *Integer* | No | Only trigger for following `conversation_id` |

It just needs to be done once, the `target_url` will receive the
events until it receives an `unsubscribe` command.

On a successful creation, Twist will return a `201 Created` and a `403
Forbidden` will be thrown if the access token scope does not have the
permission to subscribe to the specified event type.

When an event happens, we'll send a request to your `target_url` that
will be JSON encoded. The payload will be the object that triggered
the event, for example, `channel_added` will
include [the channel object](#channels).


### Unsubscribe from a hook

> Example

```shell
curl https://api.twistapp.com/api/v2/hooks/unsubscribe \
  -H "Authorization: Bearer 9b1bf97783c1ad5593dee12f3019079dbd3042cf" \
  -d target_url=https://hooks.yourdomain.com/<unique_target_url>
```

To stop listening to changes just unsubscribe your hook. The following
parameters are accepted:

| Name | Required | Description |
| --- | --- | --- |
| target_url *String* | Yes | The URL we should unsubscribe |

On a successful unsubscribe, we return a `200 OK`.

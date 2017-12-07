# Integrations

Twits has some types of integrations and you have to carefully pick
your type based on how your integration will be used. Here is a link
for the full explanation of each one with a small summary of what they
can do:

* [oAuth 2 applications](#oauth) - Requires more setup but is more powerful
* [Channel integration](#channel) - Has access to one channel only, has schedule powers
* [Thread integration](#thread) - Has access to one thread or create new threads
* [Slash command integration](#slash-command) - Receives a request when called via slash command

And below we have some information shared among all types.


### HTTPS enforcing

Twist enforces HTTPS everywhere, including our production
integrations. It means that all production URLs that communicate with
Twist somehow have to use HTTPS. If you need a certificate, we highly
recommend [Let's Encrypt](https://letsencrypt.org/). Furthermore, we
also enforce
[certificate chain check](https://support.dnsimple.com/articles/what-is-ssl-certificate-chain/).


### Outgoing webhooks

**Note**: Outgoing webhooks are not the same
as [REST Hooks](#resthooks). Resthooks are harder to setup but much
more powerful and are used by oAuth2 integrations only. Outgoing
webhooks are used by Slash command, Thread and Channel integrations.

Outgoing webhooks send data when an activity happens (e.g. a new comment is
added to the thread or an uninstall happens). We also send data when a user uses
a slash command.

Outgoing webhooks will send an HTTPS POST request to your specified URL. The
payload depends on the integration type.

Your webhooks handler can respond to add data back to Twist.

The outgoing hooks can work with any language or framework — as long as they
support HTTPS and JSON.


#### POST Parameters when users add new objects

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


#### POST Parameters when an uninstall happens

When a team uninstalls your integration, you can expect following
parameters. You can use this to clean up any state you may have on your end.

| Name | Optional | Description |
| --- | --- | --- |
| event_type *String* | No | Will be `uninstall` |
| install_id *Integer* | No | The unique id of the installation |
| workspace_id *Integer* | No | The workspace the installation belonged to |
| user_id *Integer* | No | The id of the uninstaller |
| user_name *String* | No | The full name of the uninstaller |


#### POST Parameters when a ping happens

For debugging purposes, you might get a `ping` payload. You should respond back
with a JSON `{"content": "pong"}`.

| Name | Optional | Description |
| --- | --- | --- |
| event_type *String* | No | Will be `ping` |
| user_id *Integer* | No | The id of the pinger |
| user_name *String* | No | The full name of the pinger |


#### Adding content back

If your handler wishes to post a response back, use the following JSON
response:

`{"content": "42 is the answer to everything."}`


#### Error handling

Non-200 responses will be retried 10 times in the span of 12 hours.

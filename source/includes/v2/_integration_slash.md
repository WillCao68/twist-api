# &#8627; Slash command

Slash command integrations are installed on a team level, and they add
a slash command to the system. When a user types `/command arguments`
your integration runs and can act upon the arguments.

**Examples**: `/gif funny cats` is a slash command. Another example is
the [appear.in](https://appear.in) integration, which lets you easily
schedule video meetings (`/appearin meeting-room`). Both integrations
are available on
our [integrations page](https://twistapp.com/integrations).

As slash commands can be used in different contexts (i.e. inside of a thread or conversation), the return may be different depending on where it is used. You can see the differences in the below example.


### Example implementation

> Thread

```text
# formstring data

user_name: user_name
verify_token: 200_abcdefghijklmnopqrstuvwx
thread_id: 180000
workspace_id: 4800
command_argument: appearin_username
command: /appear
thread_title: Test thread name
content: /appear appearin_username
event_type: comment
comment_id: 6402000
channel_name: General
channel_id: 6000
user_id: 9000

```

> Conversation

```text
# formstring data

user_id: 9000,
event_type: message,
conversation_title: conversation_title,
verify_token: 200_abcdefghijklmnopqrstuvwx,
content: /appear username,
command: /appear,
conversation_id: 296779,
command_argument: username,
user_name: John D.,
message_id: 3456789,
workspace_id: 1234
```

```json
# JSON return
{
    "content": "📹 [/appear appearin_username](https://appear.in/appearin_username)"
}
```

You can check some examples in the
[integration examples repository](https://github.com/Doist/twist-integration-examples/tree/master/slash_integration). Let's
use the
[python example implementation](https://github.com/Doist/twist-integration-examples/tree/master/slash_integration/python) for
the appear.in an example.

Your application will receive a POST call with some information in a
formstring format, so the integration can decide what to do and it
replies with a JSON containing a `content` key. The text on this
`content` key will replace the message containing the slash command.


### Timeout

Be aware that your integration must deliver the content in less than
**10 seconds** or the server will drop the connection and try again as
stated
in [Error handling](https://developer.twistapp.com/v2/#integrations).

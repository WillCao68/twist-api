# Action buttons

Action buttons are used inside other objects
like [threads](#threads), [comments](#comments)
or [messages](#conversation-messages). As it's possible to have many
action buttons inside the same object, they are represented as a list
of action buttons in the `actions` key.

They are used to make it easy to execute an action for the message
received. An example of usage would be adding text to the message box or a
link to another page.

> Action buttons objects:

```json
{
    ...,

    "actions": [
        {
            "action": "open_url",
            "url": "https://www.google.com",
            "type": "action",
            "button_text": "Open Url Action Btn"
        },
        {
            "action": "prefill_message",
            "message": "This message is prefilled by an action button",
            "type": "action",
            "button_text": "Prefill Message Action Btn"
        },
        {
            "action": "prefill_reply",
            "message": "This reply is prefilled by an action button",
            "type": "action",
            "button_text": "Prefill Reply Action Btn"
        },
    ],

    ...
}
```

### Properties of the action button object

| Name | Description |
| ---- | --- |
| action *String* | The action of the button. It can be **open_url**, **prefill_message**, or **prefill_reply** |
| type *String* | The type of the button, for now just `action` is available |
| button_text *String* | The text for the action button |
| message *String* | Message to be added when using __prefill_*__  actions |
| url *String* | URL to redirect. It's used for **open_url** types |


## Get action buttons

Action buttons cannot be retrieved alone, they are part of other
objects like [threads](#threads), [comments](#comments),
and [messages](#messages). To retrieve them use the get methods from
the object in which they were inserted.


## Add an action button

Action buttons cannot be added alone, they are part of other objects
like [threads](#threads), [comments](#comments),
and [messages](#messages). To add them, you have to use the add
methods from the object in which they will be inserted into.

### Parameters to add new action buttons

| Name | Required | Description |
| ---- | --- | --- |
| action *String* | Yes | The action of the button. It can be **open_url**, **prefill_message**, or **prefill_reply** |
| type *String* | Yes | The type of the button, for now just `action` is available |
| button_text *String* | Yes | The text for the action button |
| message *String* | No | Message to be added when using __prefill_*__  actions |
| url *String* | No | URL to redirect in case the action used requires it |

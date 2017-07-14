---
title: Twist API Reference

toc_footers:
  - <a href='https://twistapp.com/integrations/create'>Create your oAuth2 app</a>

includes:
  - v2/errors
  - v2/authentication
  - v2/batch
  - v2/users
  - v2/workspaces
  - v2/groups
  - v2/channels
  - v2/threads
  - v2/comments
  - v2/conversations
  - v2/conversation_messages
  - v2/attachments
  - v2/reactions
  - v2/inbox
  - v2/search
  - v2/notifications
  - v2/notification_settings
  - v2/url_join
  - v2/loop_in
  - v2/integration_types
  - v2/integration_rest_hooks
  - v2/integration_ws
  - v2/integration_configure_url
  - v2/integration_automatic_reports

search: true
---

# Introduction

Add extra functionality for your own teams or build integrations to share with others.

This is the official documentation of the Twist API.


## Authentication

Login and signup are done via `/api/v2/users/login` and `/api/v2/users/register`. For public integrations you must use our oAuth 2 authentication.


## Temporary ids

Temporary ids are negative and can be used when adding, updating or deleting items.


## Return results and error handling

A response is always a JSON object which can be following:

- On successful return: JSON data
- On an error return, HTTP error code followed by: `{ “error”: [error_code, error_string], **kwargs }`


## Dates
For dates we use ISO 8601. The formatting we can have inside the system:
- Date time: `%Y-%m-%d %H:%M:%S`
- Date only: `%Y-%m-%d`
- With timezone info: `%Y-%m-%d %H:%M:%S +00:00`

The current API should only return `%Y-%m-%d %H:%M:%S`, where the time zone is implicit set to `UTC`.

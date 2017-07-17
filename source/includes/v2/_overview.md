# Introduction

This is the official Twist API documentation, a reference to the functionality
our public API provides, with detailed description of each API endpoint, its
parameters, and examples.


## Authentication

Login and signup are done via `/api/v2/users/login` and
`/api/v2/users/register`. For public integrations you must use
our [oAuth 2 authentication](#oauth-2).


## Temporary ids

Temporary ids are negative and can be used when adding, updating or deleting
items.


## Return results and error handling

A response is always a JSON object which can be following:

- On successful return: JSON data
- On an error return, HTTP error code followed by: `{“error”: [error_code, error_string], **kwargs}`


## Dates

For dates we use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601). The
formatting we can have inside the system:

- Date time: `%Y-%m-%d %H:%M:%S`
- Date only: `%Y-%m-%d`
- With timezone info: `%Y-%m-%d %H:%M:%S +00:00`

The current API should only return `%Y-%m-%d %H:%M:%S`, where the time zone is
implicit set to `UTC`.

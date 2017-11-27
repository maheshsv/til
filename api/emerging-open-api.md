# An emerging type of Open API: webhook plugin

The most popular Open APIs on the web today are:

- RESTful API/GraphQL etc
- webhook

There is an emerging type of Open API, let me call it: **webhook plugin**. A regular webhook is an HTTP POST that usually used for notification when something happened. The main purpose is to notify third-party who registered the webhook. But for plugin webhook, you still do an HTTP request, but **it expects a specific format of response which can be used by the caller**. 
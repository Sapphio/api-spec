---
title: "Resources"
---

# Resources

* TOC
{:toc}

The App.net API is a JSON API.

Guiding principles are:

* Always return JSON. If you are using JSONP, the returned JSON will be wrapped in a function call.
* Utilize HTTP error codes and methods.
* In general, required parameters are in URLs; optional parameters are specified in the query string. **This is not always the case.**
* If we need complex data structures from you, you should send them as a JSON string. We don't need any more conventions for putting arrays and dictionaries directly into URL-encoded GET/POST values.
* We follow a convention of including the API version number in the resource path. The current API version is version 0.

## Hostname
Please use https://alpha-api.app.net/ to access the APIs.

## User

<%= render 'partials/endpoints/user' %>

## Post

<%= render 'partials/endpoints/post' %>

## Channel

<%= render 'partials/endpoints/channel' %>

## Message

<%= render 'partials/endpoints/message' %>

## File

<%= render 'partials/endpoints/file' %>

## App Stream

<%= render 'partials/endpoints/app-stream' %>

## User Stream

<%= render 'partials/endpoints/user-stream' %>

## Filter

<%= render 'partials/endpoints/filter' %>

## Interaction

<%= render 'partials/endpoints/interaction' %>

## Stream Marker

<%= render 'partials/endpoints/stream-marker' %>

## Text Processor

<%= render 'partials/endpoints/text-processor' %>

## Token

<%= render 'partials/endpoints/token' %>

## Place

<%= render 'partials/endpoints/place' %>

## Explore Stream

<%= render 'partials/endpoints/explore-stream' %>

## Configuration

<%= render 'partials/endpoints/config' %>

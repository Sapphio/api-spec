---
title: "Post Lifecycle"
---

# Post Lifecycle

* TOC
{:toc}

## Create a Post

Create a new <a href="/docs/resources/post/">Post</a> object. Mentions and hashtags will be parsed out of the post text, as will bare URLs.

You can also create a Post by sending JSON in the HTTP post body that matches the <a href="/docs/resources/post/">post schema</a> with an HTTP header of ```Content-Type: application/json```. Currently, the only keys we use from your JSON will be ```text```, ```reply_to```, ```machine_only```, ```annotations``` and ```entities```. To create complex posts (including [machine only posts](/docs/resources/post/#machine-only-posts)), you must use the JSON interface. See the [JSON example](#json-example) below. If you would like to specify your own entities, please refer to the [user specified entities](/docs/meta/entities/#user-specified-entities) documentation.

If you want to test how your text will be processed you can use the [text processor](/docs/resources/text-processor).

*Note: You cannot reply to a repost. Please reply to the parent Post.*

<%= general_params_note_for "post" %>

<%= endpoint "POST", "posts", "User", "write_post" %>

<%= post_params [
    ["text", "The raw text of the post."],
    ["reply_to", "(Optional) The id of the Post that this new Post is replying to."]
]%>

#### Example

> POST https://alpha-api.app.net/stream/0/posts
>
> DATA text=%40berg+FIRST+post+on+this+new+site+%23newsocialnetwork

~~~ js
{
    "data": {
        "id": "1", // note this is a string
        "user": {
            ...
        },
        "created_at": "2012-07-16T17:25:47Z",
        "text": "@berg FIRST post on this new site #newsocialnetwork",
        "html": "<span itemprop=\"mention\" data-mention-name=\"berg\" data-mention-id=\"2\">@berg</span> FIRST post on this new site <span itemprop=\"hashtag\" data-hashtag-name=\"newsocialnetwork\">#newsocialnetwork</span>.",
        "source": {
            "client_id": "udxGzAVBdXwGtkHmvswR5MbMEeVnq6n4",
            "name": "Clientastic for iOS",
            "link": "http://app.net"
        },
        "machine_only": false,
        "reply_to": null,
        "thread_id": "1",
        "num_replies": 0,
        "num_reposts": 0,
        "num_stars": 0,
        "entities": {
            "mentions": [{
                "name": "berg",
                "id": "2",
                "pos": 0,
                "len": 5
            }],
            "hashtags": [{
                "name": "newsocialnetwork",
                "pos": 34,
                "len": 17
            }],
            "links": []
        },
        "you_reposted": false,
        "you_starred": false
    },
    "meta": {
        "code": 200,
    }
}
~~~

<br>

#### Example (JSON Data)

> POST https://alpha-api.app.net/stream/0/posts?include_post_annotations=1
> 
> Content-Type: application/json
> 
> DATA '{"text": "@berg FIRST post on this new site #newsocialnetwork", "annotations": [{"type": "net.app.core.geolocation", "value": {"latitude": 74.0064, "longitude": 40.7142}}]}'

~~~ js
{
    "data": {
        "id": "1", // note this is a string
        "user": {
            ...
        },
        "created_at": "2012-07-16T17:25:47Z",
        "text": "@berg FIRST post on this new site #newsocialnetwork",
        "html": "<span itemprop=\"mention\" data-mention-name=\"berg\" data-mention-id=\"2\">@berg</span> FIRST post on this new site <span itemprop=\"hashtag\" data-hashtag-name=\"newsocialnetwork\">#newsocialnetwork</span>.",
        "source": {
            "client_id": "udxGzAVBdXwGtkHmvswR5MbMEeVnq6n4",
            "name": "Clientastic for iOS",
            "link": "http://app.net"
        },
        "machine_only": false,
        "reply_to": null,
        "thread_id": "1",
        "num_replies": 0,
        "num_reposts": 0,
        "num_stars": 0,
        "annotations": [
            {
                "type": "net.app.core.geolocation",
                "value": {
                    "latitude": 74.0064,
                    "longitude": 40.7142
                }
            }
        ],
        "entities": {
            "mentions": [{
                "name": "berg",
                "id": "2",
                "pos": 0,
                "len": 5
            }],
            "hashtags": [{
                "name": "newsocialnetwork",
                "pos": 34,
                "len": 17
            }],
            "links": []
        },
        "you_reposted": false,
        "you_starred": false
    },
    "meta": {
        "code": 200,
    }
}
~~~

## Delete a Post

Delete a <a href="/docs/resources/post/">Post</a>. The current user must be the same user who created the Post. It returns the deleted Post on success.

<%= general_params_note_for "post" %>

*Remember, access tokens can not be passed in a HTTP body for ```DELETE``` requests. Please refer to the [authentication documentation](/docs/authentication/#making-authenticated-api-requests).*

<%= endpoint "DELETE", "posts/[post_id]", "User", "write_post" %>

<%= url_params [
    ["post_id", "The id of the Post to delete."]
]%>

#### Example

> DELETE https://alpha-api.app.net/stream/0/posts/1

~~~ js
{
    "data": {
        "id": "1", // note this is a string
        "user": {
            ...
        },
        "created_at": "2012-07-16T17:25:47Z",
        "html": "<span itemprop=\"mention\" data-mention-name=\"berg\" data-mention-id=\"2\">@berg</span> FIRST post on <a href=\"https://join.app.net\" rel=\"nofollow\">this new site</a> <span itemprop=\"hashtag\" data-hashtag-name=\"newsocialnetwork\">#newsocialnetwork</span>.",
        "source": {
            "client_id": "udxGzAVBdXwGtkHmvswR5MbMEeVnq6n4",
            "name": "Clientastic for iOS",
            "link": "http://app.net"
        },
        "machine_only": false,
        "reply_to": null,
        "thread_id": "1",
        "num_replies": 3,
        "num_reposts": 0,
        "num_stars": 0,
        "entities": {
            "mentions": [{
                "name": "berg",
                "id": "2",
                "pos": 0,
                "len": 5
            }],
            "hashtags": [{
                "name": "newsocialnetwork",
                "pos": 34,
                "len": 17
            }],
            "links": [{
                "text": "this new site",
                "url": "https://join.app.net"
                "pos": 20,
                "len": 13
            }]
        },
        "you_reposted": false,
        "you_starred": false
    },
    "meta": {
        "code": 200,
    }
}
~~~

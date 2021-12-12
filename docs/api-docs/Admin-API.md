# Admin API

<!-- MarkdownTOC autolink="true" -->

* [Postman Collection](#postman-collection)
* [Fetch profile info](#fetch-profile-info)
* [Edit profile info](#edit-profile-info)
* [Change password](#change-password)
* [Upload logo](#upload-logo)
* [Upload banner](#upload-banner)
* [Gallery Media](#gallery-media)
    * [Fetch gallery pictures](#fetch-gallery-pictures)
    * [Add gallery picture](#add-gallery-picture)
    * [Update gallery picture](#update-gallery-picture)
    * [Delete gallery picture](#delete-gallery-picture)
* [Resources](#resources)
    * [Get resources](#get-resources)
    * [Add resource](#add-resource)
    * [Update resource](#update-resource)
    * [Delete resource](#delete-resource)
* [Events](#events)
    * [Fetch events](#fetch-events)
    * [Add event](#add-event)
    * [Update event](#update-event)
    * [Delete event](#delete-event)
* [Recruiting Events](#recruiting-events)
    * [Fetch recruiting events](#fetch-recruiting-events)
    * [Add recruiting event](#add-recruiting-event)
    * [Update recruiting event](#update-recruiting-event)
    * [Delete recruiting event](#delete-recruiting-event)
* [Frequently Asked Questions](#frequently-asked-questions)
    * [Fetch frequently asked questions](#fetch-frequently-asked-questions)
    * [Add question](#add-question)
    * [Delete question](#delete-question)

<!-- /MarkdownTOC -->

## Postman Collection
[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/d94f6e43c7f713013796?action=collection%2Fimport)


## Fetch profile info
* Description: Fetches the complete club profile from an officer user.
* Path: `GET /api/admin/profile`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "name": "Example Club",
    "link_name": "example-club",
    "owner": "exampleuser@berkeley.edu",
    "about_us": "This is something about the club.",
    "get_involved": "This is something about getting involved.",
    "banner_url": "<banner-pic-url>",
    "logo_url": "<logo-pic-url>",
    "app_required": true,
    "new_members": false,
    "num_users": 0,
    "apply_link": "https://www.apply-here-now.com",
    "apply_deadline_start": "2020-04-20T12:00:00",
    "apply_deadline_end": "2020-05-20T12:00:00",
    "recruiting_start": "2020-03-20T12:00:00",
    "recruiting_end": "2020-06-20T12:00:00",
    "tags": [1, 3, 4],
    "resources": [
        {
            "id": "example-resource",
            "name": "Example resource",
            "link": "https://www.resource.com"
        }
    ],
    "events": [
        {
            "name": "Example event",
            "link": "https://www.event.com",
            "event_start": "2020-04-20T12:00:00",
            "event_end": "2020-06-20T12:00:00",
            "description": "This is a description about example event.",
        }
    ],
    "recruiting_events": [
        {
            "name": "Example event",
            "link": "https://www.event.com",
            "virtual_link": "https://www.zoom.com/example-event",
            "event_start": "2020-04-20T12:00:00",
            "event_end": "2020-06-20T12:00:00",
            "description": "This is a description about example event.",
        }
    ],
    "social_media_links": {
        "contact_email": "example-email@gmail.com",
        "website": "http://example.com/",
        "facebook": "https://www.facebook.com/pages/example-club",
        "instagram": "https://www.instagram.com/example-club",
        "linkedin": "https://www.linkedin.com/in/example-club",
        "twitter": "https://twitter.com/example-club",
        "youtube": "https://www.youtube.com/channel/example-club",
        "github": "https://github.com/example-club",
        "behance": "https://www.behance.net/example-club",
        "medium": "https://medium.com/@example-club",
        "gcalendar": "<google-calendar-link>",
        "discord": "<discord-invite-link>"
    },
    "last_updated": "2020-10-20T12:00:00"
}
```

## Edit profile info
* Description: Edits the club profile.
* Path: `POST /api/admin/profile`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "is_reactivating": false,
    "name": "Example Club",
    "link_name": "example-club",
    "owner": "exampleuser@berkeley.edu",
    "about_us": "This is something about the club.",
    "get_involved": "This is something about getting involved.",
    "app_required": true,
    "new_members": false,
    "num_users": 0,
    "apply_link": "https://www.apply-here-now.com",
    "apply_deadline_start": "2020-04-20T12:00:00",
    "apply_deadline_end": "2020-05-20T12:00:00",
    "recruiting_start": "2020-03-20T12:00:00",
    "recruiting_end": "2020-06-20T12:00:00",
    "tags": [1, 3, 4],
    "social_media_links": {
        "contact_email": "example-email@gmail.com",
        "website": "http://example.com/",
        "facebook": "https://www.facebook.com/pages/example-club",
        "instagram": "https://www.instagram.com/example-club",
        "linkedin": "https://www.linkedin.com/in/example-club",
        "twitter": "https://twitter.com/example-club",
        "youtube": "https://www.youtube.com/channel/example-club",
        "github": "https://github.com/example-club",
        "behance": "https://www.behance.net/example-club",
        "medium": "https://medium.com/@example-club",
        "gcalendar": "<google-calendar-link>",
        "discord": "<discord-invite-link>"
    }
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Change password
* Description: Changes the current user's password without revoking all the access and refresh tokens.
* Path: `POST /api/admin/change-password`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "old_password": "exampleoldpassword",
    "new_password": "examplenewpassword",
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Upload logo
* Description: Replaces the current club's logo with a new one. Logos must respect a 1:1 aspect ratio (with a 5% deviation allowed). A 2 MB limit is imposed as well.
* Path: `POST /api/admin/upload-logo`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
    * multipart/form-data
        * `logo` - logo image
* Sample body output
```json
{
    "status": "success",
    "logo_url": "https://sproul-club-images-prod.s3-us-west-1.amazonaws.com/logo/example-club-logo.png"
}
```

## Upload banner
* Description: Replaces the current club's banner with a new one. Banners must respect a 10:3 aspect ratio (with a 5% deviation allowed). A 2 MB limit is imposed as well.
* Path: `POST /api/admin/upload-banner`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
    * multipart/form-data
        * `banner` - banner image
* Sample body output
```json
{
    "status": "success",
    "banner_url": "https://sproul-club-images-prod.s3-us-west-1.amazonaws.com/banner/example-club-banner.png"
}
```

## Gallery Media

### Fetch gallery pictures
* Description: Fetches all gallery pictures' metadata from a club.
* Path: `GET /api/admin/gallery-media`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-gallery-pic-1",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 1"
    }
]
```

### Add gallery picture
* Description: Adds a new gallery picture to the club with an image upload and a caption.
* Path: `POST /api/admin/gallery-media/photo`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "caption": "Example caption 2"
}
```
* multipart/form-data
    * `photo` - gallery image
* Sample body output:
```json
[
    {
        "id": "example-gallery-pic-1",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 1"
    },
    {
        "id": "example-gallery-pic-2",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 2"
    }
]
```

### Update gallery picture
* Description: Either replace an existing gallery picture, change the image's caption or do both at the same time.
* Path: `PUT /api/admin/gallery-media/photo/<pic-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "caption": "Example caption 3"
}
```
* multipart/form-data
    * `photo` - gallery image
* Sample body output:
```json
[
    {
        "id": "example-gallery-pic-1",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 1"
    },
    {
        "id": "example-gallery-pic-2",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 3"
    }
]
```

### Delete gallery picture
* Description: Deletes an existing gallery picture.
* Path: `DELETE /api/admin/gallery-media/<media-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-gallery-pic-2",
        "url": "<gallery-pic-url>",
        "caption": "Example caption 3"
    }
]
```

## Resources

### Get resources
* Description: Fetches all the resource links from a club.
* Path: `GET /api/admin/resources`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-resource-1",
        "name": "Example resource 1",
        "link": "http://example.com/"
    }
]
```

### Add resource
* Description: Adds a new resource link to the club profile.
* Path: `POST /api/admin/resources`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example Resource 2",
    "link": "http://example.com/"
}
```
* Sample body output:
```json
[
    {
        "id": "example-resource-1",
        "name": "Example resource 1",
        "link": "http://example.com/"
    },
    {
        "id": "example-resource-2",
        "name": "Example resource 2",
        "link": "http://example.com/"
    }
]
```

### Update resource
* Description: Updates an existing resource link.
* Path: `PUT /api/admin/resources/<resource-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example Resource 10",
    "link": "http://example.com/"
}
```
* Sample body output:
```json
[
    {
        "id": "example-resource-1",
        "name": "Example resource 10",
        "link": "http://example.com/"
    },
    {
        "id": "example-resource-2",
        "name": "Example resource 2",
        "link": "http://example.com/"
    }
]
```

### Delete resource
* Description: Deletes an existing resource link.
* Path: `DELETE /api/admin/resources/<resource-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-resource-10",
        "name": "Example resource 10",
        "link": "http://example.com/"
    }
]
```

## Events

### Fetch events
* Description: Fetches all events from the club profile.
* Path: `GET /api/admin/events`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-event-1",
        "name": "Example event 1",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Add event
* Description: Adds a new event.
* Path: `POST /api/admin/events`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example event 2",
    "link": "http://example.com/",
    "event_start": "2020-04-01T07:00:00.000Z",
    "event_end": "2020-08-01T07:00:00.000Z",
    "description": "This is something about the event."
}
```
* Sample body output:
```json
[
    {
        "id": "example-event-1",
        "name": "Example event 1",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    },
    {
        "id": "example-event-2",
        "name": "Example event 2",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Update event
* Description: Updates an existing event.
* Path: `PUT /api/admin/events/<event-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example event 10",
    "link": "http://example.com/",
    "event_start": "2020-04-01T07:00:00.000Z",
    "event_end": "2020-08-01T07:00:00.000Z",
    "description": "This is something about the new event."
}
```
* Sample body output:
```json
[
    {
        "id": "example-event-1",
        "name": "Example event 10",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the new event."
    },
    {
        "id": "example-event-2",
        "name": "Example event 2",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Delete event
* Description: Deletes an existing event.
* Path: `DELETE /api/admin/events/<event-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-event-10",
        "name": "Example event 10",
        "link": "http://example.com/",
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the new event."
    }
]
```

## Recruiting Events

### Fetch recruiting events
* Description: Fetches all recruiting events from the club profile.
* Path: `GET /api/admin/recruiting-events`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-recruiting-event-1",
        "name": "Example recruiting event 1",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": false,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Add recruiting event
* Description: Adds a new recruiting event.
* Path: `POST /api/admin/recruiting-events`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example recruiting event 2",
    "link": "http://example.com/",
    "virtual_link": "https://zoom.com/example-link",
    "invite_only": true,
    "event_start": "2020-04-01T07:00:00.000Z",
    "event_end": "2020-08-01T07:00:00.000Z",
    "description": "This is something about the event."
}
```
* Sample body output:
```json
[
    {
        "id": "example-recruiting-event-1",
        "name": "Example recruiting event 1",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": false,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    },
    {
        "id": "example-recruiting-event-2",
        "name": "Example recruiting event 2",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": true,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Update recruiting event
* Description: Updates an existing recruiting event.
* Path: `PUT /api/admin/recruiting-events/<event-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Example recruiting event 10",
    "link": "http://example.com/",
    "virtual_link": "https://zoom.com/example-link",
    "invite_only": false,
    "event_start": "2020-04-01T07:00:00.000Z",
    "event_end": "2020-08-01T07:00:00.000Z",
    "description": "This is something about the new event."
}
```
* Sample body output:
```json
[
    {
        "id": "example-recruiting-event-1",
        "name": "Example recruiting event 10",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": false,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the new event."
    },
    {
        "id": "example-recruiting-event-2",
        "name": "Example recruiting event 2",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": false,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the event."
    }
]
```

### Delete recruiting event
* Description: Deletes an existing recruiting event.
* Path: `DELETE /api/admin/recruiting-events/<event-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-recruiting-event-10",
        "name": "Example recruiting event 10",
        "link": "http://example.com/",
        "virtual_link": "https://zoom.com/example-link",
        "invite_only": false,
        "event_start": "2020-04-01T07:00:00.000Z",
        "event_end": "2020-08-01T07:00:00.000Z",
        "description": "This is something about the new event."
    }
]
```

## Frequently Asked Questions

### Fetch frequently asked questions
* Description: Fetches all questions and answers from the club profile.
* Path: `GET /api/admin/faq`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-question-1",
        "question": "Example question 1",
        "answer": "Example answer 1"
    }
]
```

### Add question
* Description: Adds a new question.
* Path: `POST /api/admin/faq`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
        "id": "example-question-2",
        "question": "Example question 2",
        "answer": "Example answer 2"
}
```
* Sample body output:
```json
[
    {
        "id": "example-question-1",
        "question": "Example question 1",
        "answer": "Example answer 1"
    },
    {
        "id": "example-question-2",
        "question": "Example question 2",
        "answer": "Example answer 2"
    }
]
```

### Delete question
* Description: Deletes an existing question.
* Path: `DELETE /api/admin/faq/<question-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "id": "example-question-1",
        "question": "Example question 1",
        "answer": "Example answer 1"
    }
]
```

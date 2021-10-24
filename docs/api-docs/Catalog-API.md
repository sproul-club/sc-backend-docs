# Catalog API

<!-- MarkdownTOC autolink="true" -->

- [Postman Collection](#postman-collection)
- [Fetch set of tags](#fetch-set-of-tags)
- [Fetch set of "# of users" tags](#fetch-set-of--of-users-tags)
- [Fetch organizations](#fetch-organizations)
- [Fetch specific organization](#fetch-specific-organization)

<!-- /MarkdownTOC -->

## Postman Collection
[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/8125621e08eb17533248)


## Fetch set of tags
* Description: Fetches the set of club tags
* Path: `GET /api/catalog/tags`
* Sample body output:
```json
[
    {
        "id": 42,
        "name": "Example tag"
    },
    {
        "id": 84,
        "name": "Another Example Tag"
    }
]
```

## Fetch set of "# of users" tags
* Description: Fetches the set of "number of users" tags
* Path: `GET /api/catalog/num-user-tags`
* Sample body output:
```json
[
    {
        "id": 42,
        "value": "1-100"
    },
    {
        "id": 84,
        "name": "100+"
    }
]
```

## Fetch organizations
* Description: Fetches the list of organizations without filters, sorted alphabetically.
* Path: `GET /api/catalog/organizations?limit={limit}&skip={skip}`

* Sample body output:
```json
{
    "results": [
        {
            "name": "Example Club",
            "link_name": "example-club",
            "about_us": "This is something about the club.",
            "banner_url": "<banner-pic-url>",
            "logo_url": "<logo-pic-url>",
            "app_required": true,
            "new_members": false,
            "num_users": 0,
            "tags": [1, 3, 4],
            "last_updated": "2020-10-20T12:00:00",
            "apply_deadline_end": "2020-05-20T12:00:00",
        }
    ],
    "num_results": 1
}
```

## Fetch specific organization
* Description: Fetches all information of a single organization
* Path: `GET /api/catalog/organizations/<org-id>`
* Sample body output:
```json
{
    "name": "Example Club",
    "link_name": "example-club",
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
    "reactivated": false,
    "reactivated_last": null,
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
    "recommended_clubs": [
        {
            "name": "Example Club 1",
            "link_name": "example-club-1",
            "logo_url": "<logo-pic-url>"
        },
        {
            "name": "Example Club 2",
            "link_name": "example-club-2",
            "logo_url": "<logo-pic-url>"
        },
        {
            "name": "Example Club 3",
            "link_name": "example-club-3",
            "logo_url": "<logo-pic-url>"
        },
    ],
    "last_updated": "2020-10-20T12:00:00"
}
```

# Monitor API

<!-- MarkdownTOC -->

* [Postman Collection](#postman-collection)
* [Managing Account](#managing-account)
    * [Login user](#login-user)
    * [Refresh access token](#refresh-access-token)
    * [Revoke access token](#revoke-access-token)
    * [Revoke refresh token](#revoke-refresh-token)
* [Fetch statistics](#fetch-statistics)
    * [Fetch sign up statistics](#fetch-sign-up-statistics)
    * [Fetch activity statistics](#fetch-activity-statistics)
    * [Fetch social media link usage](#fetch-social-media-link-usage)
    * [Fetch club application status usage](#fetch-club-application-status-usage)
    * [Fetch logo / banner usage](#fetch-logo--banner-usage)
* [Manage RSO emails](#manage-rso-emails)
    * [Fetch list of RSO emails](#fetch-list-of-rso-emails)
    * [Download list of RSO emails](#download-list-of-rso-emails)
    * [Add RSO email](#add-rso-email)
    * [Remove RSO email](#remove-rso-email)
* [Manage clubs](#manage-clubs)
    * [Fetch list of clubs](#fetch-list-of-clubs)
    * [Download list of clubs](#download-list-of-clubs)
    * [Remove club](#remove-club)
* [Manage club tags](#manage-club-tags)
    * [Fetch club tags with usage stats](#fetch-club-tags-with-usage-stats)
    * [Download club tags with usage stats](#download-club-tags-with-usage-stats)
    * [Add club tag](#add-club-tag)
    * [Edit club tag](#edit-club-tag)
    * [Remove club tag](#remove-club-tag)

<!-- /MarkdownTOC -->

## Postman Collection
[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/d47d615f5d4300519226?action=collection%2Fimport)

## Managing Account

### Login user
* Description: Logs in an existing admin user.
* Path: `POST /api/monitor/login`
* Sample body input:
```json
{
    "email": "exampleuser@berkeley.edu",
    "password": "examplepassword"
}
```
* Sample body output:
```json
{
    "access": "<access_token>",
    "access_expires_in": 900,
    "refresh": "<refresh_token>",
    "refresh_expires_in": 86400
}
```
* Note: `expires_in` values are just example values. Do not assume that the documentation here describes the correct `expires_in` values.

### Refresh access token
* Description: Fetches a new access token given a valid refresh token.
* Path: `POST /api/monitor/refresh`
* Headers:
    - `Authorization: Bearer <refresh_token>`
* Sample body output:
```json
{
    "access": "<access_token>",
    "access_expires_in": 900
}
```
* Note: `expires_in` values are just example values. Do not assume that the documentation here describes the correct `expires_in` values.

### Revoke access token
* Description: Revokes an issued access token, preventing further use of it.
* Path: `DELETE /api/monitor/revoke-access`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "status": "success",
    "message": "Access token revoked!"
}
```

### Revoke refresh token
* Description: Revokes an issued refresh token, preventing further use of it.
* Path: `DELETE /api/monitor/revoke-refresh`
* Headers:
    - `Authorization: Bearer <refresh_token>`
* Sample body output:
```json
{
    "status": "success",
    "message": "Refresh token revoked!"
}
```

## Fetch statistics

### Fetch sign up statistics
* Description: Fetches the sign up statistics for all user account types.
* Path: `GET /api/monitor/overview/stats/sign-up`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "club_admin": {
        "main": {
            "clubs_registered": 400,
            "clubs_confirmed": 300,
            "clubs_reactivated": 200,
            "clubs_rso_list": 1000,
        },
        "changed": {
            "clubs_registered": 100,
            "clubs_confirmed": 50,
            "clubs_reactivated": 25,
        },
        "history": {
            "clubs_registered": 300,
            "clubs_confirmed": 250,
            "clubs_reactivated": 175,
        }
    },
    "student": {
        "main": {
            "students_signed_up": 500,
            "students_confirmed": 400,
        },
        "changed": {
            "students_signed_up": 100,
            "students_confirmed": 50
        }
    }
}
```

### Fetch activity statistics
* Description: Fetches the number of active users and recent catalog searches (WIP).
* Path: `GET /api/monitor/overview/stats/activity`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "active_club_admins": 5,
    "active_students": 25,
    "catalog_searches": "N/A"
}
```

### Fetch social media link usage
* Description: Fetches the aggregated usage of social media links across all clubs.
* Path: `GET /api/monitor/more-stats/social-media`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "website": 130,
    "facebook": 191,
    "instagram": 179,
    "linkedin": 167,
    "twitter": 53,
    "youtube": 14,
    "github": 153,
    "behance": 84,
    "medium": 162,
    "gcalendar": 140,
    "discord": 41,
}
```

### Fetch club application status usage
* Description: Fetches aggregated statistics for club application statuses.
* Path: `GET /api/monitor/more-stats/club-reqs`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "app_required": 150,
    "no_app_required": 30,
    "new_members": 120,
    "no_new_members": 60,
}
```

### Fetch logo / banner usage
* Description: Fetches the aggregated usage of logo / banner pictures for clubs.
* Path: `GET /api/monitor/more-stats/pic-stats`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "logo_pic": 150,
    "no_logo_pic": 30,
    "banner_pic": 120,
    "no_banner_pic": 60,
}
```

## Manage RSO emails

### Fetch list of RSO emails
* Description: Fetches the list of RSO emails scraped from CalLink.
* Path: `GET /api/monitor/rso/list`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "email": "exampleclubemail_1@gmail.com",
        "registered": true,
        "confirmed": false
    },
    {
        "email": "exampleclubemail_2@gmail.com",
        "registered": false,
        "confirmed": false
    }
]
```

### Download list of RSO emails
* Description: Downloads a CSV file of the list of RSO emails scraped from CalLink.
* Path: `GET /api/monitor/rso/download`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample file output:
```csv
email,registered,confirmed
exampleclubemail_1@gmail.com,Yes,No
exampleclubemail_2@gmail.com,No,No
```

### Add RSO email
* Description: Adds a new RSO email.
* Path: `POST /api/monitor/rso`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "email": "exampleadmin@berkeley.edu"
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

### Remove RSO email
* Description: Removes an existing RSO email.
* Path: `DELETE /api/monitor/rso/<email>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "status": "success"
}
```

## Manage clubs

### Fetch list of clubs
* Description: Fetches the list of clubs with relevent info (abridged).
* Path: `GET /api/monitor/club/list`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "name": "Random EECS dude #254",
        "email": "exampleclubemail_1@gmail.com",
        "confirmed": true,
        "reactivated": true
    },
    {
        "name": "Popeye the Sailor Man",
        "email": "exampleclubemail_2@gmail.com",
        "confirmed": true,
        "reactivated": false
    }
]
```

### Download list of clubs
* Description: Downloads a CSV file of the list of clubs with relevent info (abridged).
* Path: `GET /api/monitor/club/download`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample file output:
```csv
name,email,confirmed,reactivated
Random EECS dude #254,exampleclubemail_1@gmail.com,Yes,Yes
Popeye the Sailor Man,exampleclubemail_2@gmail.com,Yes,No
```

### Remove club
* Description: Removes an existing officer user and thus, their respective club.
* Path: `DELETE /api/monitor/club/<email>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "status": "success"
}
```

## Manage club tags

### Fetch club tags with usage stats
* Description: Fetches the list of club tags with usage statistics per tag.
* Path: `GET /api/monitor/tags/list`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
[
    {
        "name": "ASUC",
        "num_clubs": 3
    },
    {
        "name": "Social Good",
        "num_clubs": 55
    },
    {
        "name": "Technology",
        "num_clubs": 30
    }
]
```

### Download club tags with usage stats
* Description: Downloads a CSV file of the list of club tags with usage statistics per tag.
* Path: `GET /api/monitor/tags/download`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample file output:
```csv
_id,name,num_clubs
0,ASUC,3
1,Social Good,55
2,Technology,30
```

### Add club tag
* Description: Adds a new club tag.
* Path: `POST /api/monitor/tags`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Education"
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

### Edit club tag
* Description: Edits an existing club tag.
* Path: `DELETE /api/monitor/tags/<tag-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body input:
```json
{
    "name": "Community Service"
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

### Remove club tag
* Description: Removes an existing club tag, if there are no clubs using said tag.
* Path: `DELETE /api/monitor/tags/<tag-id>`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "status": "success"
}
```

# User API
We use JWTs to manage authentication, mainly for allowing the user to edit their club's information.

<!-- MarkdownTOC autolink="true" -->

* [Postman Collection](#postman-collection)
* [Does email exist? \(before sign up\)](#does-email-exist-before-sign-up)
* [Is password strong enough? \(before sign up\)](#is-password-strong-enough-before-sign-up)
* [Register a new user](#register-a-new-user)
* [Resend confirmation email](#resend-confirmation-email)
* [Confirm new user](#confirm-new-user)
* [Login user](#login-user)
* [Request password reset](#request-password-reset)
* [Confirm password reset](#confirm-password-reset)
* [Refresh access token](#refresh-access-token)
* [Revoke access token](#revoke-access-token)
* [Revoke refresh token](#revoke-refresh-token)

<!-- /MarkdownTOC -->

## Postman Collection
[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/9313a243aa286cd566dd?action=collection%2Fimport)


## Does email exist? (before sign up)
* Description: Checks if a given email exists within our list of scraped CalLink emails.
* Path: `POST /api/user/email-exists`
* Sample body input:
```json
{
    "email": "exampleuser@berkeley.edu"
}
```
* Sample body output:
```json
{
    "exists": true
}
```

## Is password strong enough? (before sign up)
* **NOTE**: This endpoint needs to be secured or reworked ASAP!!!
* Description: Checks if a given password is strong enough.
* Path: `POST /api/user/password-strength`
* Sample body input:
```json
{
    "password": "p@ssw0rd!"
}
```
* Sample body output:
```json
{
    "strong": true
}
```

## Register a new user
* Description: Registers a new officer user and a corresponding club.
* Path: `POST /api/user/register`
* Sample body input:
```json
{
    "name": "Example Club",
    "email": "exampleuser@berkeley.edu",
    "password": "examplepassword",
    "tags": [3, 1, 4],
    "app_required": true,
    "new_members": true,
    "num_users": 0
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Resend confirmation email
* Description: Resends a new confirmation email if the user exists.
* Path: `POST /api/user/resend-confirm`
* Sample body input:
```json
{
    "email": "exampleuser@berkeley.edu",
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Confirm new user
* Description: Confirms the new officer user. This endpoint link is normally within the confirmation email.
* Path: `GET /api/user/confirm/<confirm_token>`
* Result: Redirects you to the club edit profile page

## Login user
* Description: Logs in an existing officer user.
* Path: `POST /api/user/login`
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

## Request password reset
* Description: Sends a password reset email to the user's email.
* Path: `POST /api/user/request-reset`
* Sample body input:
```json
{
    "email": "exampleuser@berkeley.edu"
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Confirm password reset
* Description: Resets the officer user's password and revokes all existing access and refresh tokens.
* Path: `POST /api/user/confirm-reset`
* Sample body input:
```json
{
    "token": "<reset-password-token>",
    "password": "examplepassword",
}
```
* Sample body output:
```json
{
    "status": "success"
}
```

## Refresh access token
* Description: Fetches a new access token given a valid refresh token.
* Path: `POST /api/user/refresh`
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

## Revoke access token
* Description: Revokes an issued access token, preventing further use of it.
* Path: `DELETE /api/user/revoke-access`
* Headers:
    - `Authorization: Bearer <access_token>`
* Sample body output:
```json
{
    "status": "success",
    "message": "Access token revoked!"
}
```

## Revoke refresh token
* Description: Revokes an issued refresh token, preventing further use of it.
* Path: `DELETE /api/user/revoke-refresh`
* Headers:
    - `Authorization: Bearer <refresh_token>`
* Sample body output:
```json
{
    "status": "success",
    "message": "Refresh token revoked!"
}
```

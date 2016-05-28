---
title: API Reference

language_tabs:
  - postman

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>


search: true
---

# Introduction

Welcome to the Nope API! You can use our API to access Nope API endpoints, which can get information on users and in our database.

You can view request/reseponse examples in the dark area to the right.

# User 

This section documents API's in the nope ecosystem that allow the manipulation of users in the system.
Operations allowed are read, create and update.

## Create

```postman
POST "http://replacewithhost.com/api/user"
```

> The above command accepts a JSON request payload structured like this:

```json
{
  "user_name": "john_snow",
  "profile_picture_url": "https://s3-us-west-1.amazonaws.com/nope-nc/iknownothing.jpg",
  "email": "john_snow@got.com",  #Required
  "first_name": "John",
  "last_name": "Snow"
}
```
> Response

```json
{
  "user": {
    "uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
    "user_name": "john_snow",
    "email": "john_snow@got.com",
    "phone_number": null,
    "password": null,
    "first_name": "John",
    "last_name": "Snow",
    "created_at": "2016-05-27T07:32:33.828786Z",
    "updated_at": "2016-05-27T07:32:33.828826Z",
    "user_login_type": "facebook",
    "is_active": true,
    "profile_picture_url": "https://s3-us-west-1.amazonaws.com/nope-nc/iknownothing.jpg"
  },
  "is_registered": false
}
```
This endpoint creates a new user.

Check the section on the right for api request-response samples.

### HTTP Request

`POST http://replacewithhost.com/api/user`

<aside class="notice">
When a user_name is not provided, the api generates one for you. This will most likely be the username part of the email
that preceedes the '@'. 
</aside>

The is_registered field in the response specifies if a user is new or an existing user. If the value of the
parameter is false, the user signing up is a new user. The value of this parameter should be used by the mobile app
in the first/login screen to determine if the user can be directed to the nope feeds or whether she/he has to go through
the signup flow.

<aside class="success">
A successfull user creation call will also log you into the system!!!
</aside>

## Edit

```postman
PUT "http://replacewithhost.com/api/user"
```

> The above command accepts a JSON request payload structured like this:

```json
{
  # None of the fields are mandatory.
  "user_name": "john_snow",
  "profile_picture_url": "https://s3-us-west-1.amazonaws.com/nope-nc/iknownothing.jpg",
  "first_name": "John1",
  "last_name": "Snow1"
}
```
> Response

```json
{
  "user": {
    "uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
    "user_name": "john_snow",
    "email": "john_snow@got.com",
    "phone_number": null,
    "password": null,
    "first_name": "John1",
    "last_name": "Snow1",
    "created_at": "2016-05-27T07:32:33.828786Z",
    "updated_at": "2016-05-27T07:32:33.828826Z",
    "user_login_type": "facebook",
    "is_active": true,
    "profile_picture_url": "https://s3-us-west-1.amazonaws.com/nope-nc/iknownothing.jpg"
  },
  "is_registered": false
}
```
This endpoint updates an existing user.

Check the section on the right for api request-response samples.

### HTTP Request

`POST http://replacewithhost.com/api/user`

<aside class="notice">
You will have to be logged in to make this api request. The user being edited is the user that
is logged in.
</aside>

The is_registered field in the response specifies if a user is new or an existing user. If the value of the
parameter is false, the user signing up is a new user. The value of this parameter should be used by the mobile app
in the first/login screen to determine if the user can be directed to the nope feeds or whether she/he has to go through
the signup flow.

<aside class="success">
Check response to make sure that the user was successfully udpated.
</aside>

## Exists

```postman
HEAD "http://replacewithhost.com/api/user/exists?user_name=john_snow"
```

> The above request accepts user_name as a query parameter.

This endpoint updates an existing user.

### HTTP Request

`POST http://replacewithhost.com/api/user/exists`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
user_name | no default | Check if value already exists as username

Since this is a HEAD request, there won't be a response body.
Check the HTTP status for a 200 status code. If the status code is 200,
the user name exists and cannot be used. If the status code is 404, 
the username can be used.

<aside class="success">
Check response to make sure that the user was successfully udpated.
</aside>


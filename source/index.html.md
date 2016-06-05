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

This endpoint is used to check if a username already exists in the database.

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

#Nope
This section documents API's in the nope ecosystem that allow the manipulation of nopes in the system.
Operations allowed are read, create.

## Create

```postman
POST "http://replacewithhost.com/api/nope"
```

> The above request accepts a JSON request payload structured like this:

```json
{
  "text": "hello",
  "image_url": "http://linkwithimage.com/yo.jpg",
  "video_url": "http://linkwithvideo.com/yo.mpg",
  "tags": ["yo", "yo1"],
  "location": {
      "lat": "121.00",
      "lon": "23.00"
  }
}
```
> Response

```json
{
  "uuid": "cbc12d07-9e76-4a8d-94bc-3b54dac38957",
  "user_uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
  "text": "hello",
  "created_at": "2016-06-05T05:47:21.444387Z",
  "updated_at": "2016-06-05T05:47:21.444427Z",
  "video_url": "http://linkwithvideo.com/yo.mpg",
  "image_url": "http://linkwithimage.com/yo.jpg",
  "tags": "[u'yo', u'yo1']",
  "location": "{u'lat': u'121.00', u'lon': u'23.00'}",
  "number_of_comments": 0,
  "liked_count": 0,
  "disliked_count": 0
}
```
This endpoint creates a new nope.

Check the section on the right for api request-response samples.

### HTTP Request

`POST http://replacewithhost.com/api/nope`

<aside class="notice">
Include session cookie with request. The user details are derived from the cookie.
</aside>

The image and the video url must be retrieved before making the call to create a nope.
The resources should either be uploaded to s3 using the AWS mobile client or you could also
use the upload api provided in the media section for this purpose.

## Get

```postman
GET "http://replacewithhost.com/api/nope?page=1"
```

> Response

```json
[
  {
    "uuid": "cfa327d2-e05e-400a-926f-346fa683ef48",
    "user_uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
    "text": "hello",
    "created_at": "2016-06-04T19:06:45.032113Z",
    "updated_at": "2016-06-04T19:06:45.032189Z",
    "video_url": null,
    "image_url": null,
    "tags": "[u'yo', u'yo1']",
    "location": "[24.567, 54.678]",
    "number_of_comments": 4,
    "liked_count": 0,
    "disliked_count": 0,
    "has_liked": false,
    "has_disliked": false
  },
]
```

This endpoint gets all the nopes in a paginated fashion.

Check the section on the right for api request-response samples.

### HTTP Request

`GET http://replacewithhost.com/api/nope`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Page Number

<aside class="notice">
Include session cookie with request. The user details are derived from the cookie.
</aside>

When there are no more pages to show, the server throws a status code of 416

## Add Comment
```postman
POST "http://replacewithhost.com/api/nope/nope_uuid/comment"
```

> The above request accepts a JSON request payload structured like this:

```json
{
  "text": "hello"
}
```
> No response body. Returns "201 Created" on success


This api lets you create a comment for a specific nope.

Check the section on the right for api request-response samples.

### HTTP Request

`GET http://replacewithhost.com/api/nope/cfa327d2-e05e-400a-926f-346fa683ef48/comment`

### Path Parameters

Parameter | Description
--------- | -----------
nope_uuid | Uuid of the nope being commented upon

<aside class="notice">
Include session cookie with request. The user details are derived from the cookie.
</aside>

There is no response body for this api.

<aside class="success">
If the action was successful, you will receive a HTTP status code of 201.
</aside>

## Get Comments
```postman
POST "http://replacewithhost.com/api/nope/nope_uuid/comments"
```
```json
\\This is the response
{
  "comments": [
    {
      "uuid": "dd4612ad-5c3f-4e1b-9c18-40b781121dc8",
      "text": "Yo yo",
      "user_uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
      "created_at": "2016-06-04T19:11:19.034778Z",
      "updated_at": "2016-06-04T19:11:19.034843Z",
      "nope": "cfa327d2-e05e-400a-926f-346fa683ef48"
    },
    {
      "uuid": "f5b82d42-df50-4f6f-8376-96dd660ecbb9",
      "text": "Yo yo",
      "user_uuid": "0d549302-de2f-4c04-bc8e-0b3b967892f5",
      "created_at": "2016-06-04T19:58:01.868574Z",
      "updated_at": "2016-06-04T19:58:01.868649Z",
      "nope": "cfa327d2-e05e-400a-926f-346fa683ef48"
    },
  ]
}
```

This api will get all comments associated to the nope

Check the section on the right for api request-response samples.

### HTTP Request

`GET http://replacewithhost.com/api/nope/cfa327d2-e05e-400a-926f-346fa683ef48/comments`

### Path Parameters

Parameter | Description
--------- | -----------
nope_uuid | Uuid of the nope

<aside class="notice">
Include session cookie with request. The user details are derived from the cookie.
</aside>


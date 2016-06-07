---
title: API Reference

language_tabs:
  - cURL

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the documentation for Loops API!

This API is a RESTFUL API built in Flask. All body requests/responses will be in JSON. JWT Tokens are used to authenticate users.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To pass your JWT token when making a request, use the following header:

```shell
curl "URLYOUWISHTOACCESS"
  -H "JWT-Auth: test"
```

Loop uses JWT tokens to authenticate users. You can generate a JWT token using the '/authtoken/' endpoint.

<aside class="notice">
You must replace <code>test</code> with your personal API key.
</aside>

# User's

## Sign Up

```shell
curl "http://localhost:500/users/" -XPOST
  -H "Content-Type: application/json" 
  -d {"username": "USERNAMEHERE", "password": "PASSWORDHERE"}
```

> The above request envokes a JSON response like this:

```json
{
  "uuid": "YOURUUID"
}
```

This endpoint signs a user up.

### HTTP Request

`POST http://localhost:5000/users/`

## Users profile information

```shell
curl "http://localhost:5000/users/idofuser/" -XGET
```

> The above request envokes a JSON response like this:

```json
{
  "username": "USERNAME OF USER",
  "bio": "BIO OF USER",
  "name": "NAME OF USER",
  "all posts": "NUMBER OF ALL POSTS (INT)",
  "active posts": "NUMBER OF ACTIVE POSTS (INT)",
  "profile_picture": "LINK TO USERS PROFILE PICTURE",
  "old posts": "NUMBER OF OLD POSTS (INT)",
  "id": "ID OF USER"
}
```

This endpoint returns a users profile information.

### HTTP Request

`GET http://localhost:5000/users/idofuser/`

##Users Posts

```shell
curl "http://localhost:5000/users/idofuser/posts/?filter=all" -XGET
```

> the above request envokes a JSON response like this:

```json
{
  "active": [
    {
      "votes": "NUMBER OF VOTES (INT)",
      "user_id": "USERID",
      "area": "AREA ID",
      "media": "LINK TO POSTS MEDIA",
      "y": "Y AXIS OF TEXT ON SCREEN (INT)",
      "lifetime": "LIFETIME OF POST (INT)",
      "message": "MESSAGE OF POST",
      "id": "ID OF POST",
      "time_uploaded": "TIME OF POST UPLOAD"
    }
  ],
  "old": [
    {
      "votes": "NUMBER OF VOTES (INT)",
      "user_id": "USERID",
      "area": "AREA ID",
      "media": "LINK TO POSTS MEDIA",
      "y": "Y AXIS OF TEXT ON SCREEN (INT)",
      "lifetime": "LIFETIME OF POST (INT)",
      "message": "MESSAGE OF POST",
      "id": "ID OF POST",
      "time_uploaded": "TIME OF POST UPLOAD"
    },
  ]
}

```

```shell
curl "http://localhost:5000/users/idofuser/posts/?filter=old" -XGET
```

> the above request envokes a JSON response like this:

```json
[
  {
	"votes": "NUMBER OF VOTES (INT)",
	"user_id": "USERID",
	"area": "AREA ID",
	"media": "LINK TO POSTS MEDIA",
	"y": "Y AXIS OF TEXT ON SCREEN (INT)",
	"lifetime": "LIFETIME OF POST (INT)",
	"message": "MESSAGE OF POST",
	"id": "ID OF POST",
	"time_uploaded": "TIME OF POST UPLOAD"
  }
]
```

```shell
curl "http://localhost:5000/users/idofuser/posts/?filter=active" -XGET
```

> the above request envokes a JSON response like this:

```json
[
  {
	"votes": "NUMBER OF VOTES (INT)",
	"user_id": "USERID",
	"area": "AREA ID",
	"media": "LINK TO POSTS MEDIA",
	"y": "Y AXIS OF TEXT ON SCREEN (INT)",
	"lifetime": "LIFETIME OF POST (INT)",
	"message": "MESSAGE OF POST",
	"id": "ID OF POST",
	"time_uploaded": "TIME OF POST UPLOAD"
  }
]
```

This endpoint returns all posts of a specific user

### HTTP Request 

`GET http://localhost:5000/users/idofuser/posts/`

### Query Parameters

Parameter | Values | Description
--------- | ------- | -----------
filter | active | Returns all active posts
filter | old | Returns all active posts
filter | all | Returns all posts old and active

## Username Check

```shell
curl "http://localhost:5000/usernamecheck/?username=USERNAMETOCHECK" -XGET
```

> The above request envokes a JSON response like this:

```json
{
  "isAvailable": true
}
```

This endpoint returns True/False if a username is in use or not.

### HTTP Request 

`GET http://localhost:5000/usernamecheck/`

### Query Parameters

Parameter | Values |
--------- | ------- |
username | username you want to check |

## User Search

```shell
curl "http://localhost:500/users/search/?query=USERNAMEYOUWANTTOSEARCH"
```

> The above request envokes a JSON response like this:

```json
[
  {
    "username": "USERNAME OF USER",
    "bio": "BIO OF USER",
    "profile_picture": "URL TO PROFILE PICTURE OF USER",
    "id": "ID OF USER",
    "name": "NAME OF USER"
  }
]
```
This endpoint will search for users with a given username.

### HTTP Request

`GET http://localhost:5000/users/search/'

### Query Parameters

Parameter | Values |
--------- | ------- |
query | username you want to search |

## Updating user information 

```shell
curl "http://localhost:5000/users/idofuser/" -H "JWT-Auth: YOURJWTTOKEN"
	-H "Content-Type: application/json" 
	-d '{"name": "DESIRED NAME CHANGE", "email": "EMAIL YOU WISH TO CHANGE", "bio": "BIO YOU WISH TO CHANGE"}'
	-XPATCH
```

> The above request enokes a JSON response like this:

```json
{
  "message": "Your profile has been updated"
}
```

This endpoint will update a users profile information.

<aside class="warning">You must include all JSON keys in the request. If you do not wish to change a key value be sure to keep it the same as its current value.</aside>

### HTTP Request

`PATCH http://localhost:5000/users/idofuser`

## Updating user information and profile picture

```shell
curl "http://localhost:5000/users/idofuser/" -H "JWT-Auth: YOURJWTTOKEN"
	-F 'user_data={"name": "DESIRED NAME CHANGE", "email": "EMAIL YOU WISH TO CHANGE", "bio": "BIO YOU WISH TO CHANGE"}'
	-F 'file=@filepath'
	-XPATCH
```

> The above request envokes a JSON response like this:

```json
{
  "message": "Your profile has been updated"
}
```

This endpoint will update a users profile information. It can also update their profile picture as shown in the curl request.

<aside class="warning">You must include all JSON keys in the request. If you do not wish to change a key value be sure to keep it the same as its current value.</aside>

### HTTP Request

`PATCH http://localhost:5000/users/idofuser`

## Deleting user account

```shell
curl "http://localhost:5000/users/idofuser/" -H "JWT-Auth: YOURJWTTOKEN"
	-H "Content-Type: application/json"
	-d '{"password": "YOUR PASSWORD"}'
	-XDELETE
```

> The above request enokes a JSON response like this:

```json
{
  "message": "Your profile has been deleted!"
}
```

This endpoint well delete a users account 

### HTTP request

`DELETE http://localhost:5000/users/idofuser`

# Loop's

## Saving a Loop

## Getting your saved Loop's

## Nearby Loop's

## Searching for Loop's

## Loop's posts

# Post's

##Trending posts

## Voting on a post

## Deleting a post

## Posting to a Loop

# Custom Loop's

## Creating Custom Loop

## Private custom Loop access



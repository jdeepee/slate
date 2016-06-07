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

`PATCH http://localhost:5000/users/idofuser/`

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

```shell 
curl "http://localhost:5000/loops/nearby/?lat=YOURLAT&lon=YOURLONG&filter=cityorschool"
	-XGET
```

> The above request envokes a JSON response like this:

```json
[
  {
    "state": "CA",
    "name": "San Francisco",
    "loopid": 5391959
  }
]
```

```shell 
curl "http://localhost:5000/loops/nearby/?lat=YOURLAT&lon=YOURLONG&filter=custom"
	-XGET
```

> The above request envokes a JSON response like this:

```json
[
  {
    "city": "San Francisco",
    "name": "Test Custom Open Loop",
    "country": "US",
    "creator_id": "d87beafe-b7ad-479c-95a8-66b4ba2e1caf",
    "private": "false",
    "state": "CA",
    "location": "true",
    "city_short": "SF",
    "id": "4f3d001c-d9dd-4752-89f9-5ad82d1c8c4e"
  }
]
```

This endpoint will search for nearby Loops with given filters.


Parameter | Description
--------- | -----------
lat | The latitude of your location
lon | The longitude of you location
filter | The type of Loops you wish to return

### HTTP Request

`GET http://localhost:5000/loops/nearby/`

## Searching for Loop's

```shell 
curl "http://localhost:5000/loops/search/?lat=YOURLAT&lon=YOURLONG&filter=cityorschool&query=nameoflooptofind"
	-XGET
```

> The above request envokes a JSON response like this:

```json
[
  {
    "country": "US",
    "state": "CA",
    "name": "San Francisco",
    "loopid": 5391959
  }
]
```

```shell 
curl "http://localhost:5000/loops/search/?lat=YOURLAT&lon=YOURLONG&filter=custom&query=nameoflooptofind"
	-XGET
```

> The above request envokes a JSON response like this:

```json
[
  {
    "city": "San Francisco",
    "name": "Test Custom Open Loop",
    "country": "US",
    "creator_id": "d87beafe-b7ad-479c-95a8-66b4ba2e1caf",
    "private": "false",
    "state": "CA",
    "location": "true",
    "city_short": "SF",
    "id": "4f3d001c-d9dd-4752-89f9-5ad82d1c8c4e"
  }
]
```

This endpoint will search all Loops by name and return them based on distance from you.

Parameter | Description
--------- | -----------
lat | The latitude of your location
lon | The longitude of you location
filter | The type of Loops you wish to return
query | Name of Loop you wish to find 

### HTTP Request

`GET http://localhost:5000/loops/search/`

## Loop's posts

# Post's

##Trending posts

## Voting on a post

## Deleting a post

## Posting to a Loop

# Custom Loop's

## Creating Custom Loop

```shell
curl "http://localhost:5000/loops/create/" -H "JWT-Auth: YOURJWTTOKEN"
	-H "Content-Type: application/json"
	-d '{
		    "name": "DESIRED NAME",
		    "latitude": "DESIRED LAT",
		    "longitude": "DESIRED LONG",
		    "location": "true/false",
		    "private": "true/false"
		}'
	-XPOST
```

> The above request envokes a JSON response like this:

```json
{
  "message": "Loop successfully created"
}
```

This endpoint will allow you to create a custom Loop

<aside class="warning">Location and private must be set to either 'true' or 'false'.</aside>

### HTTP Request

`POST http://localhost:5000/loops/create/`

## Private custom Loop access

```shell 
curl "http://localhost:5000/loops/LOOPID/confirm/"
	-H "JWT-Auth: YOURJWTTOKEN"
	-H "Content-Type: application/json"
	-d '{"user": "IDOFUSERYOUWISHTOAUTHENTICATEINTOLOOP"}'
	-XPOST
```

> The above request envokes a JSON response like this;

```json
{
  "message": "User has been accepted into the loop!"
}
```

This endpoint allows the owner of a private loop to add users into the Loop.

<aside class="warning">You must be the owner of the Loop to add people to the Loop.</aside>

### HTTP Request

`POST http://localhost:5000/loops/LOOPID/confirm/`

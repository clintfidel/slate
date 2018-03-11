---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# WELCOME TO WEconnect

# Introduction

WEconnect provides a platform that brings businesses and individuals together. This platform creates awareness for businesses and gives the users the ability to write reviews about the businesses they have interacted with. WEconnect provides opportunities for users to gain experience while exploring the app, users are also not limited as to the kind of business that should be shared, viewed or reviwed. This platform provides various users with the kind of business within thier jurisdiction as it has the search functionality that is aimed at providing convinece to users while having great time on the app.

# Development

The application was developed with [NodeJs](http://nodejs.org) and [Express](http://expressjs.com) is used for routing.

# Installation

1. Ensure you have NodeJs and PostgreSQL installed
2. Clone the repository `https://github.com/clintfidel/WEconnect.git`
3. Change your directory `cd WEconnect`
4. Install all dependencies `npm install`
5. Start the app `npm start` for development Or
6. Use [postman] to consume the API

# Authentication

WEconnect uses (username and password) to login to allow access to the API protected routes. On registering or login, a token is generated to secure the users details.
WEconnect expects that the token is included in the header or body as `x-access-token: token` as failure to do so would term the users as `unauthenticated` thereby granting him/her no access to the protected routes. All API requests to the server are stated below

# Api Summary

## Below are the API endpoints and their functions

EndPoint                                                |   Functionality
--------------------------------------------------------|------------------------
POST /api/v1/auth/signup                                |   Create a new users.
POST /api/v1/auth/login                                 |   Logs in existing users.
PUT /api/v1/auth/editprofile/:id                        |   Edit profile.
POST /api/v1/businesses/                                |   Adds news business
GET /api/v1/businesses                                  |   Get all users business
GET /api/v1/businesses/:id                              |   Get one user business
GET /api/v1/businesses?location=keyword                 |   Get business based on search query
GET /api/v1/businesses?category=keyword                 |   Get business based on search query
PUT /api/v1/businesses/:id/                             |   Modify user business profile
DELETE /api/v1/businesses/:id                           |   Delete user business profile
POST /api/v1/businesses/:businessId/reviews             |   Post reviews
GET /api/v1/business/:businessId/reviews                |   Get all reveiws a business has

# Users

## Sign up User
### Request

  * Endpoint: Post: `/api/v1/auth/signup`
  * Body  `(application/json)`
  
### Response
  * Status: `201 created` 
  * Body  `(application/json)`

> Request:

```json
{
    "username": "Clinton",
    "fullname": "Fidelis clinton",
    "email": "clintonfidelis@gmail.com",
    "password": "password"
},
```

> Response:

```json

{
    "message": "signed up successfully",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRlZFVzZXIiOnsiaWQiOjIsImZ1bGxuYW1lIjoiRmlkZWxpcyBDbGludG9uIiwidXNlcm5hbWUiOiJDbGludGZpZGVsMSIsImVtYWlsIjoiQ2xpbnRmaWRlbDFAZ21haWwuY29tIiwicGFzc3dvcmQiOiIkMmEkMTAkUkp1b0svQ1lCa1EuWWRIVmZkRmdndWRHSTQxc09FWkU5SWFZQjlmSU9BSFJ3cVY3V0lnR3EifSwiZXhwaXJlc0luIjp7ImV4cCI6IjFociJ9LCJpYXQiOjE1MjA3Njg3MTh9.52FFp9iRS-GUzOCaJq3U61Zzra_KqvNaL49AwtEN7vw"
}

```

## Sign in User
### Request
  * Endpoint: Post: `/api/v1/users/signin` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Request:

```json
{
    "username": "Clinton",
    "password": "password"
},
```

> Response:

```json
{
    "message": "logged in successfully",
        "token":  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRlZFVzZXIiOnsiaWQiOjIsImZ1bGxuYW1lIjoiRmlkZWxpcyBDbGludG9uIiwidXNlcm5hbWUiOiJDbGludGZpZGVsMSIsImVtYWlsIjoiQ2xpbnRmaWRlbDFAZ21haWwuY29tIiwicGFzc3dvcmQiOiIkMmEkMTAkUkp1b0svQ1lCa1EuWWRIVmZkRmdndWRHSTQxc09FWkU5SWFZQjlmSU9BSFJ3cVY3V0lnR3EifSwiZXhwaXJlc0luIjp7ImV4cCI6IjFociJ9LCJpYXQiOjE1MjA3Njg3MTh9.52FFp9iRS-GUzOCaJq3U61Zzra_KqvNaL49AwtEN7vw"

}

```



## Edit user details

### Request
  * Endpoint: put: `/api/v1/auth/editprofile/:id` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Request:

```json
{
    "username": "clintfidel",
    "fullname": "Andela Andela",
    "email": "clint.fidel@andela.com",
    "password": "Anddela2018"
},

```
<aside class="notice">You should provide your token to the header or body as you would not be granted permission if token is not found....You should also edit the details as you so please,
dont also forget to include your user id in the params.
</aside>

> Response

```json
{
    "message": "user profile updated successfully",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjoxLCJmdWxsbmFtZSI6IkFuZGVsYSBBbmRlbGEiLCJ1c2VybmFtZSI6ImNsaW50RklERUwiLCJlbWFpbCI6ImNsaW50LmZpZGVsQGFuZGVsYS5jb20iLCJwYXNzd29yZCI6IiQyYSQxMCRhNk1RakN4Z3h2Uk8yOGNxamVtTnMuQnc5LzA1c3VtR0pZbUc1bjlCVXpBYWRaLm8yRzJCRyJ9LCJleHBpcmVzSW4iOnsiZXhwIjoiMWhyIn0sImlhdCI6MTUyMDc3MjkyNn0.-tOpxNWLD4F0iDiGCSpta14wWaDAj_k1ER4K0AeacdM"
}

```

# Business

## Adds new Business
### Request

  * Endpoint: Post: `/api/v1/businesses/`
  * Body  `(application/json)`
  
### Response
  * Status: `201 created`
  * Body  `(application/json)`

> Request:

```json
{
    "name": "andelabusiness",
    "location": "nairobi",
    "categoryId": 2,
    "details": "andela again and again" ,
},
```
<aside class="notice">token must be included in the header or body to access protected routes (x-access-token: token)</aside>

> Response:

```json

{
    "message": "Business created successfully",
    "businessProfile": {
        "id": 3,
        "name": "andelabusiness",
        "details": "andela again and again",
        "location": "nairobi",
        "categoryId": 7,
        "views": 0,
        "userId": 3,
        "createdAt": "2018-03-28T23:34:26.617Z",
        "updatedAt": "2018-03-28T23:34:26.617Z",
        "Category": {
            "category": "others"
        }
    }
}
```

## Edit user business profile

### Request
  * Endpoint: put: `/api/v1/businesses/1` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Request:

```json
{
  "name": "andelabusiness1",
    "location": "categoryId",
    "categoryId": 3,
    "details": "andela again and again" ,
},

```
<aside class="notice">You should provide your token to the header or body as you would not be granted permission if token is not found....You should also edit the details as you so please,
dont also forget to include your business id in the params.
</aside>

> Response

```json
{
    "status": "success",
    "message": "Business successfully edited",
    "data": {
        "name": "andelabusiness1",
        "details": "andela again and again",
        "location": "nairobi",
        "categoryId": 2,
        "userId": 3
    }
}
```

## Get all businesses

### Request
  * Endpoint: Get: `/api/v1/businesses/` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Response:

```json

{
    "status": "Success",
    "Businesses": [
        {
            "id": 7,
            "name": "Business5",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "Niger",
            "categoryId": 2,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:50:10.906Z",
            "updatedAt": "2018-03-27T22:50:10.906Z"
        },
        {
            "id": 8,
            "name": "Business6",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "south Africa",
            "categoryId": 7,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:50:53.484Z",
            "updatedAt": "2018-03-27T22:50:53.484Z"
        },
        {
            "id": 9,
            "name": "Business7",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "Togo",
            "categoryId": 10,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:51:11.702Z",
            "updatedAt": "2018-03-27T22:51:11.702Z"
        },
        {
            "id": 10,
            "name": "Andela",
            "details": "I love andela",
            "location": "Nigeria",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T15:39:42.327Z",
            "updatedAt": "2018-03-28T15:39:42.327Z"
        },
        {
            "id": 5,
            "name": "Business3",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "London",
            "categoryId": 4,
            "views": 2,
            "userId": 2,
            "createdAt": "2018-03-27T22:47:24.299Z",
            "updatedAt": "2018-03-28T17:11:29.395Z"
        },
        {
            "id": 11,
            "name": "6757565757",
            "details": "htrr hgh fgh fgh hg hfgh fghf rrgrt hfgh ghf h",
            "location": "76767868687",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T17:31:15.433Z",
            "updatedAt": "2018-03-28T17:31:15.433Z"
        },
        {
            "id": 12,
            "name": "AndelaAndela",
            "details": "I love andela",
            "location": "Nigeria",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T17:54:55.718Z",
            "updatedAt": "2018-03-28T17:54:55.718Z"
        },
        {
            "id": 13,
            "name": "1234556",
            "details": "I love andela",
            "location": "Nigeria",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T17:55:07.263Z",
            "updatedAt": "2018-03-28T17:55:07.263Z"
        },
        {
            "id": 14,
            "name": "7up and pepsi",
            "details": "htrr hgh fgh fgh hg hfgh fghf rrgrt hfgh ghf h",
            "location": "Abuja",
            "categoryId": 5,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T20:54:31.888Z",
            "updatedAt": "2018-03-28T20:54:31.888Z"
        },
        {
            "id": 15,
            "name": "andelabusiness1",
            "details": "andela again and again",
            "location": "nairobi",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T23:34:26.617Z",
            "updatedAt": "2018-03-28T23:41:24.620Z"
        }
    ]
}

```
## Get one business

### Request
  * Endpoint: Get: `/api/v1/businesses/9` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Response:

```json

 {
            "id": 9,
            "name": "Business7",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "Togo",
            "categoryId": 10,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:51:11.702Z",
            "updatedAt": "2018-03-27T22:51:11.702Z"
        },

```

## Get all businesses based on search query(location)

### Request
  * Endpoint: Get: `/api/v1/businesses?location=Togo` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Response:

```json
{
    "message": "Business Found!",
    "Businesses": [
        {
            "id": 9,
            "name": "Business7",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "Togo",
            "categoryId": 10,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:51:11.702Z",
            "updatedAt": "2018-03-27T22:51:11.702Z",
            "User": {
                "username": "ruqoyah1"
            },
            "Category": {
                "category": "entertainment"
            }
        }
    ]
}

```

## Get all businesses based on search query(category)

### Request
  * Endpoint: Get: `/api/v1/business?category=Fashion` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

<aside class="notice">You should provide your token to the header or body as you would not be granted permission if token is not found....You should also edit the details as you so please, dont also forget to include your user id in the body and busness id in the params.
</aside>

> Response:

```json

{
    "message": "Business Found!",
    "Businesses": [
        {
            "id": 7,
            "name": "Business5",
            "details": "We are a global technological company that is aimed at solving human and artificial problems and creating new opportunites",
            "location": "Niger",
            "categoryId": 2,
            "views": 0,
            "userId": 2,
            "createdAt": "2018-03-27T22:50:10.906Z",
            "updatedAt": "2018-03-27T22:50:10.906Z",
            "User": {
                "username": "ruqoyah1"
            },
            "Category": {
                "category": "fashion"
            }
        },
        {
            "id": 10,
            "name": "Andela",
            "details": "I love andela",
            "location": "Nigeria",
            "categoryId": 2,
            "views": 0,
            "userId": 3,
            "createdAt": "2018-03-28T15:39:42.327Z",
            "updatedAt": "2018-03-28T15:39:42.327Z",
            "User": {
                "username": "Andela"
            },
            "Category": {
                "category": "fashion"
            }
        },
        {
}

```

## Delete a businesss

### Request
  * Endpoint: Delete: `/api/v1/business/1` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

<aside class="notice">You should provide your token to the header or body as you would not be granted permission if token is not found....You should also edit the details as you so please, dont also forget to include your user id in the body and busness id in the params.
</aside>

> Response:

```json

{
    "message": "Business deleted successfully",
    "id": 5
}

```

# Review

## Adds new Review to business
### Request

  * Endpoint: Post: `/api/v1/business/:businessId/reviews`
  * Body  `(application/json)`
  
### Response
  * Status: `201 created`
  * Body  `(application/json)`

> Request:

```json
{
  "userId": 1,
  "content": "This is really helpful"
}

```

> Response:

```json

{
    "message": "you have successfully reviewed this business",
    "review": {
        "id": 2,
        "businessId": "1",
        "userId": "1",
        "comments": "i think i can relate with this"
    }
}

```
## Get all review for a business

### Request
  * Endpoint: Get: `api/v1/business/:businessId/reviews` 
  * Body  `(application/json)`

### Response
  * Status: `200 ok` 
  * Body  `(application/json)`

> Response:

```json

{
    "status": "success",
    "businessdata": {
        "id": 1,
       "name": "Andela",
       "location": "Nigeria",
       "categoryId": 2,
       "AllReviews": {
    "review": [
        {
            "id": 1,
            "userId": 1,
            "businessId": 1,
            "comments": "This is really helpful"
        }
        {
            "id": 1,
            "userId": 2,
            "businessId": 1,
            "comments": "i really can relate to this"
        }
    ]
}

```
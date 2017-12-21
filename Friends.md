# iOKids Friends API

The iOKids Profile API allows authenticated users to retrieve their list of iOKids friends. Developers can test the API 
with a free [developer account](https://sandbox.iokids.net/developer). Partners can use the friends API to retrieve basic 
profile information for friends iOKids users.

Developers can review the [detailed API specification](https://app.swaggerhub.com/apis/iOKids/Friends/1.0.0) on SwaggerHub. 
The friends API returns the public profile information for the user's friends. For details on the profile data structure,
please review the [Profile API](/Profile.md) definition.

Call the friends route with a GET request:

`GET https://sandbox.iokids.net/v1/my/friends`

A successful call returns a status of 200 and the following data structure:

```
[
    {
        "userId": "7a30d2da9956431c899321a53b3ab653",
        "handle": "@user1",
        "firstName": "User",
        "lastName": "One",
        "country": "us",
        "userType": "child"
    },
    {
        "userId": "d2ccfb039bbb4492997542a82ef68aa2",
        "handle": "@user2",
        "firstName": "User",
        "lastName": "Two",
        "country": "us",
        "userType": "child"
    }
]
```

For users that have an invalid token, a status of 401 is returned with:
```
{
    "error_code": "4010",
    "error_description": "Access token invalid"
}
```

For children who do not have parental permission to use an application, the following is returned with a status of 401:
```
{
    "error_code": "4011",
    "error_description": "Application does not have permission"
}
```


APIs and Documentation - Copyright 2017, Dynepic Inc. - All rights reserved

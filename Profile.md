# iOKids Profile API

The iOKids Profile API allows authenticated users to pull information from their profile. Developers can test the API 
with a free [developer account](https://sandbox.iokids.net/developer). Partners can use the profile to retrieve profile
information for iOKids users.

Developers can review the [detailed API specification](https://app.swaggerhub.com/apis/iOKids/Profile/1.0.0) on SwaggerHub. 

The profile makes the following information about iOKids users available:

| Data Element | Element Name | Description |
| ------------ | ------------ | ----------- |
| Handle | handle | The iOKids User Name |
| First Name | firstName | First Name |
| Last Name | lastName | Last Name |
| Country | country | 2-character country identifier, e.g. 'us' |
| User Type | userType | The type of user. Will be one of "child", "teen-minor", or "adult". Child users are subject to additional controls on iOKids and in your Application |
| User Identifier | userId | An identifier for this user that is unique among all users associated with your application (client id). This is not a universally unique identifier. |

Future versions of the profile API may include information about the guardian if the user is a child.

Call the profile route with a GET request:

`GET https://sandbox.iokids.net/v1/my/profile`

If you are using the self-contained sandbox running in a docker container:

`GET http://localhost:9000/v1/my/profile`

A successful call returns a status of 200 and the following data structure:

```
{
    "userId": "7a30d2da9956431c899321a53b3ab653",
    "handle": "@user1",
    "firstName": "User",
    "lastName": "One",
    "country": "us",
    "userType": "child"
}
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

# iOKids Challenge API

The iOKids Challenge API allows authenticated users to challenge another iOKids user to a competition. Developers of games
will use this API to allow user to invite other iOKids users to play the game. If the challenged user does not have the 
game on their device, they will be prompted to download it from the Apple App store or Google Play store. 

Developers can test the API with a free [developer account](https://sandbox.iokids.net/developer).

This version of the challenge API is simple: it communicates to iOKids which UserId your application user is challenging.
iOKids will handle the data flow:

* Notify the iOKids user they have been challenged!
* If the iOKids user does not have the 3rd party application installed, a notification is sent to the user or parent to 
download the app from the app store.
* If the challengee is a child, iOKids will manage the required parental approvals

After the challenged user logs in, they can retrieve a list of their challenges

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

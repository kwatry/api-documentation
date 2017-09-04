# iOKids User Profile API

**For use in testing iOKids Social Sign-On**

While the full specification for the iOKids User Profile is in work, developers testing the iOKids Social Sign-On
can make the following call to the sandox APIs:

`GET https://sandbox.iokids.net/my/profile`

If you are using the self-contained sandbox running in a docker container:

`GET http://localhost:9000/my/profile`

A successful call returns a status of 200 and the following data structure:

```
{
    "userId": "7a30d2da9956431c899321a53b3ab653",
    "handle": "@user1",
    "firstName": "User",
    "lastName": "One"
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

# iOKids Search API

The iOKids Search API allows authenticated users to find other users of your application using a search term. The search 
term will look for matches against the first name, last name, and handle fields of profiles who have used your application.

Developers can review the [detailed API specification](https://app.swaggerhub.com/apis/iOKids/Search/1.0.0) on SwaggerHub. 
The search API returns the public profile information for users who match the search term. For details on the profile 
data structure, please review the [Profile API](/Profile.md) definition.

Search with a GET request using the searchTerm attribute:

`GET https://sandbox.iokids.net/user/v1/search?term=SEARCH_TERM`

A successful call returns a status of 200 and the following data structure:

```
{
    "docs": [
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
    ],
    "page": 1,
    "total": 2
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

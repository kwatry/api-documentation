# Running an iOKids Mock SSO Server

Developers can test the [iOKids Social Sign-On](iOKids-SSO.md) flow on their development machines with the help of the 
iOKids Mock SSO Server available via via [docker container](https://hub.docker.com/r/dynepic/iokids-sso-mock-server/).

## Run the Mock Server

1. If you don't already have the docker client, download and install it for your operating system (stable channel recommended):

    * [Mac OS X](https://docs.docker.com/docker-for-mac/install/)
    * [Windows](https://docs.docker.com/docker-for-windows/install/)
    
2. With Docker running, open the command line and type:

    `docker run -p:"9000:9000" dynepic/iokids-sso-mock-server:latest`

That's it! You now have mock iOKids SSO services running at [http://localhost:9000/](http://localhost:9000/). Open the link 
a browser and you should see `iOKids Mock SSO Server`.

## Test the SSO Flow

You can test the SSO flow using the free [Postman](https://www.getpostman.com/) application. After installing Postman:

1. Create a new request. Use "GET" as the method and set the URL to `http://localhost:9000/v1/my/profile`.
2. On the Authorization tab, select `OAuth 2.0` from the Authorization *Type* drop-down.
3. After selecting OAuth 2.0, click the new button called `Get New Access Token` and use the following as values:

    | Parameter | Value |
    | --------- | ----- |
    | Token Name | iOKids Reference |
    | Auth URL | http://localhost:9000/oauth/signin |
    | Access Token URL | http://localhost:9000/oauth/token |
    | Client ID | select one from the list below, e.g.<br/>35bcf547e2884a6995be87c94509eb92 |
    | Client Secret | select the corresponding secret below, e.g.<br/>d322e25c0cbd411fbda832ae94aa3aaf |
    | Scope | profile |
    | Grant Type | Authorization Code |
    | Request access token locally? | Yes (check the box) |
    
4. Click the button `Request Token`. 
5. In response, a window is displayed with the Mock SSO Server log-in. Select credentials from the list below, 
e.g. username: @user1, password: OAuthTest.
6. After log-in, the window asks if the user wants to grant access to the iOKids profile. Select `Grant`. 
7. The window will close and Postman has received the new token. Click on `iOKids Reference` in the Auth2 list to view
the token.
8. In the "Add token to" drop-down, select "Header" and click `Use Token`. Note that on the Header tab, Postman has added
the token as a Bearer token in the Authorization header.
9. Click the blue `Send` button to send the request with the OAuth token.

You should receive a basic user profile in response:
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

## Mock Clients (companies) and Users

<a name="user-data"></a>The mock server supports two companies:

| Field | Company 1 | Company 2 | Notes |
| ----- | --------- | --------- | ----- |
| Client ID | 35bcf547e2884a6995be87c94509eb92 | d77d83fee0f84cd3a18137ad4c6a23de | Used in the OAuth configuration |
| Client Secret | d322e25c0cbd411fbda832ae94aa3aaf | 787558e2188240548f6d5d8a306180bd | Used in the OAuth configuration |
| Redirect URIs | http://localhost:3000/callback<br /> https://www.getpostman.com/oauth2/callback | http://localhost:3000/callback<br /> https://www.getpostman.com/oauth2/callback | Use the localhost address in your OAuth configuration. <br />Postman value required for local Postman testing |
| Customer Name | ACME, Inc. | Gamification, Inc. | The name of the company appears on the log-in and permission screens |
| App Name | ACME Useful App | Addictive Games | The name of the application appears on the log-in and permission screens |

And three users:

| User ID | Handle (Log-in) | First Name | Last Name | Password | Notes |
| ------- | --------------- | ---------- | --------- | -------- | ----- |
| 7a30d2da9956431c899321a53b3ab653 | @user1 | User | One | OAuthTest | |
| d2ccfb039bbb4492997542a82ef68aa2 | @user2 | User | Two | OAuthTest | |
| 502befd88c2d469987cbd50531abca5a | @user3 | User | Three | OAuthTest | This user can authenticate but never has permissions to use the profile service. The service always returns a 4011 error. |


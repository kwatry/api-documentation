#### Implementation Details for iOKids OAuth Flow
This documentation reviews the http calls and data exchange that form the iOKids Social Sign-On (OAuth 2.0) flow. 

**Authorization Request**

Display an iOKids Log-in to the user. In calling the log-in link, the web server application will identify itself with
its client id. 

```
GET https://sso.iokids.net/oauth/signin?response_type=code
&client_id=CLIENT_ID
&redirect_uri=CALLBACK_URL
&scope=profile
&state=NONCE
```

A call to authorize includes these request parameters:
* **response_type** - always 'code' for the web server application flow
* **client_id** - your client id, found in the iOKids partner dashboard
* **redirect_uri** - after login, iOKids will redirect back to a URL on your site. This URI must be pre-registered in the 
partner dashboard.
* **scope** - a space delimited list of iOKids scopes for which your application is requesting access. This list must be 
one of the defined iOKids Scopes below and be registered in the partner dashboard as scopes your application will request
* **state** - a string value provided by the web server application that maintains state between the authorization request 
and the iOKids server response. The value will be returned as a request parameter to the 
redirect URI and should be validated by the web server. This may be a nonce or base64 encoded object with information 
relevant for the web server application

**Authorization Prompt**

In response to the authorization request, a web page login form for iOKids is displayed. The user logs in and decides 
whether or not to allow to your app. After the user decides, iOKids will redirect to the redirect_uri provided in the 
initial request. 

`GET https://REDIRECT_URI/callback?code=AUTH_CODE&state=NONCE`

In the case of a failed login or denial of permissions, an error is returned:

`GET https://REDIRECT_URI/callback?error=access_denied`

**Token Request**

Using the AUTH_CODE, the web server application will retrieve an access token.

```
POST https://sso.iokids.net/oauth/token
    grant_type=authorization_code&
    code=AUTH_CODE&
    redirect_uri=REDIRECT_URI&
    client_id=CLIENT_ID&
    client_secret=CLIENT_SECRET
```

The call to request a token includes these parameters posted in the request body:
* **grant_type** - always 'authorization_code' for a token request using an authorization code
* **code** - the authorization code provided by the iOKids server
* **redirect_uri** - the callback URL provided to generate the authorization code. iOKids verifies the redirect_uri was
pre-registered in the partner dashboard and the one used to generate the authorization code.
* **client_id** - your client id, found in the partner dashboard
* **client_secret** your client secret, found in the partner dashboard

The response from iOKids will be:

```
{
    "access_token": "ACCESS_TOKEN",
    "refresh_token": "REFRESH_TOKEN",
    "expires_in": 3600,
    "token_type": "Bearer"
}
```

* **access_token** - the iOKids access token to use in API calls. Use this token in the "Authorization" header as follows:
    ```Authorization: Bearer ACCESS_TOKEN``` 
    The access token is a JSON Web Token which can be decoded to retrieve a unique identifier of the iOKids user.    
* **refresh_token** - once the access token expires, the web server application can retrieve a new one with the refresh 
token (see below)
* **expires_in** - in how many seconds the access token will expire

**Refresh Token Request**

Make a call to the token URL to refresh an access token:

```
POST https://sso.iokids.net/oauth/token
    grant_type=refresh_token&
    refresh_token=REFRESH_TOKEN&
    client_id=CLIENT_ID&
    client_secret=CLIENT_SECRET
```

The call to request a token includes these parameters posted in the request body:
* **grant_type** - always 'refresh_token' for a token request using a refresh token
* **refresh_token** - the refresh token provided by the iOKids server in response to a token request
* **client_id** - your client id, found in the partner dashboard
* **client_secret** your client secret, found in the partner dashboard

## JWT Token

### Header
| Field | Name | Value | Description |
| ----- | ---- | ----- | ----------- |
| alg | Algorithm | RS256 | iOKids currently uses RS256 |
| typ | Token Type | jwt | The type of token will always be jwt |

### Body
| Field | Name | Value | Description |
| ----- | ---- | ----- | ----------- |
| iss | Issuer | sso.iokids.net | The JWT issuer. This value must be **sso.iokids.net** |
| aud | Audience | [your client id] | The audience for this token. This value must be your client id. If it isn't, this token should be rejected. |
| sub | Subject | | The unique identifier for this iOKids user |
| exp | Expiration Time | [milliseconds since unix epoch] | The time at which this token is no longer valid |
| iat | Issued At | [milliseconds since unix epoch] | The time the token was issued. |
| jti | Unique Identifier | | The unique identifier for this token. |

### Signature
The signature should be validated by the OAuth client using the key(s) found in the [iOKids JSON Web Keys Set](https://sso.iokids.net/.well-known/jwks.json). 

`example jwt...`
 
APIs and Documentation - Copyright 2017, Dynepic Inc. - All rights reserved
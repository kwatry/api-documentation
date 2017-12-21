# Application User Data API

Application developers can use the iOKids Application User Data API to store and retrieve user-specific data for the logged-in
user. For example, a game developer may store a user's game history, average score, current level, and other user-specific
data. Developers can also share data between users in a bucket. Buckets are used to track shared interactions between
users, for example in multi-user game play or when two users interact.

Developers can test the API with a free [developer account](https://sandbox.iokids.net/developer). Partners can use 
the API to ensure all user-specific application data is COPPA and GDPR compliant.

Developers can review the [detailed Application User Data API specification](https://app.swaggerhub.com/apis/iOKids/ApplicationUserData/1.0.0) on SwaggerHub. 

This server's primary mode of interaction is via websockets.  API users should utilize a websocket connection for each
user that wishes to interact with app data and app buckets. Developers can optionally use the RESTful API (see 
definition below), however data buckets are only available through the websocket interface for now. 

## Websocket Usage

### Connecting

With native websockets:

`let client = new WebSocket('<server-url>v1/userdata/ws?authorization=' + <sso-auth-token>);`

Note: Alternately, clients can user the exposed [Primus](https://github.com/primus/primus) js library: `<server-url>/ws/primus.js`

This will create a websocket connection for app data and bucket messages.  Then, you will need to listen for messages
and errors:

```javascript
client.on('message', (message) => {
  let data = JSON.parse(message);
});

client.on('error', (err) => {
  // handle error (auth error, for example)
});
```

Upon initialization, the server will send an initialization success message, then sync the user's app data and current
buckets.

```javascript
client.on('message', (message) => {
  let data = JSON.parse(message);
  if (message.type === 'status' && message.subtype === 'initialization' && message.success) {
    // Socket is initialized and ready
  } else if (message.subtype === 'data') {
    // App Data sync message
    // Example (initial sync after connecting):
    // {
    //   type: 'update',
    //   subtype: 'data',
    //   path: '',
    //   data: {}, (JSON)
    //   success: true
    // }
    // Example (data updated remotely):
    // {
    //   type: 'update',
    //   subtype: 'data',
    //   path: 'path.to.updated.field',
    //   data: 'new value', (can be JSON, string, number, etc.)
    //   success: true
    // }
    // Example (data was sent to the server on this channel):
    // {
    //   type: 'update',
    //   subtype: 'data',
    //   path: null,
    //   data: 'data sync success',
    //   success: true
    // }
  } else if (message.subtype === 'bucket') {
    // Bucket sync message, same structure as app data messages
  } else if (message.type === 'error') {
    // Non-halting error (for example, a sync failure)
  }
});
```
All messages have the following structure:
```
{
  type: 'create', 'update', or 'delete',
  subtype: 'data' or 'bucket',
  success: Boolean,
  path: String, a dot path of the location in the data structure that has been updated, optional for some messages,
  data: payload, can be any valid JSON type
}
```

Note that for bucket updates, the 'path' parameter will include the name of the bucket followed by a "/" character, then
the dot path of the update in the bucket's JSON data structure.

### Sending Data to the Server via Socket

After connecting your socket and receiving the data sync message, you can send updates to the channel user's app data
as following (assuming the "client" is a Primus client):

```javascript
client.write({
  type: 'update',
  subtype: 'data',
  path: 'key',
  data: 'new value!'
});
```

If the update is successful, you will receive a message as follows:

```
{
  type: 'update',
  subtype: 'data',
  path: null,
  data: 'data sync success',
  success: true
}
```

Any other users listening to the updated user's app data will receive an update message:

```
{
  type: 'update',
  subtype: 'data',
  path: 'key',
  data: 'new value!',
  success: true
}
```

### Working With Buckets

Buckets are shared app data spaces for a list of registered users.  Buckets can be created on any channel, but only a
user who is registered in a bucket's user list can delete a bucket.

#### Creating and Updating a Bucket

After initializing a user's websocket, a bucket can be created on the socket as follows:

```javascript
client.write({
  type: 'create',
  subtype: 'bucket',
  path: 'bucket-name',
  data: {
    users: [/* Array of API user Ids */]
  }
});
```

The `data.users` field tells the server what users should be subscribed to the bucket.  If the bucket is created, all
the users in the list (except the bucket's creator) will receive a message like this:

```
{
  type: 'update',
  subtype: 'bucket',
  path: 'bucket-name/',
  data: {},
  success: true
}
```

From then on, upon subscribing all the users will get the current state of the bucket in a sync message.  Any updates to
the bucket will produce similar update messages to all users in the "users" list.

To update the data in a bucket, the message is almost identical to an app data update:

```javascript
client.write({
  type: 'update',
  subtype: 'bucket',
  path: 'bucket-name/path.to.value',
  data: 'new value!'
});
```

Similarly, this will produce an "update" message to all users in the bucket's "users" list.  The sending channel will
receive a message as follows:

```
{
  type: 'update',
  subtype: 'bucket',
  path: 'bucket-name/path.to.value',
  data: 'data sync success',
  success: true
}
```

#### Deleting a Bucket

Any user in the "users" list of a bucket can delete it.  To delete a bucket, send the following message:

```javascript
client.write({
  type: 'delete',
  subtype: 'bucket',
  path: 'bucket-name',
  data: null
});
```

If the delete is successful, all users in the list will receive a message like this:

```
{
  type: 'delete',
  subtype: 'bucket',
  path: 'bucket-name',
  data: 'Bucket deleted',
  success: true
}
```

##Using the REST Interface

Store user-specific data with a PUT request. The single sign-on authentication token uniquely identifies the application 
and user so only the custom data object is required. A successful PUT results in a 200 with no response data.

```
PUT https://sandbox.iokids.net/v1/userdata

{
    "level": 6,
    "badgesEarned: ["rookie", "pro"]
    "games": [
        { 
            "name": "Pro Tournament Miami"
            "score": 2100
        },
        {
            "name": "Pro Tournament Seatle"
            "score": 3200
        }
    ]
}
```

Retrieve user-specific data with a GET request. The single sign-on token uniquely identifies the application and user so
no further data is required. A successful call returns a status of 200 and the custom data structure:

```
GET https://sandbox.iokids.net/v1/userdata

{
    "level": 6,
    "badgesEarned: ["rookie", "pro"]
    "games": [
        { 
            "name": "Pro Tournament Miami"
            "score": 2100
        },
        {
            "name": "Pro Tournament Seatle"
            "score": 3200
        }
    ]
}
```

A delete is performed with a DELETE request. A successful call returns a status of 200.

`DELETE https://sandbox.iokids.net/v1/userdata`

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

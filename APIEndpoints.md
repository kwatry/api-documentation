# API Endpoints

iOKids provides a production "live" environment and a sandbox environment for testing. API endpoints are constructed by
combining the environment and the API path. Details are listed below.

| Environment | URI | Description |
| ----------- | --- | ----------- |
| Production | https://api.iokids.net/ | Live environment. All published apps should consume APIs from this URI. |
| Sandbox | https://sandbox.iokids.net/ | Test environment. Apps in testing should use this URI. |


| API | Path(s) | Description | Swagger Docs |
| --- | ------- | ----------- | ------------ | 
| Authorization | oauth/signin <br/> oauth/token | iOKids Social Sign-on | [Sign-On Flow](/iOKids-SSO.md) |
| Profile | user/v1/my/profile <br/> user/v1/my/profile/cover <br/> user/v1/my/kids | Profile API | [swagger doc](https://app.swaggerhub.com/apis/iOKids/Profile/1.0.0) |
| Friends | user/v1/my/friends | Friends API | [swagger doc](https://app.swaggerhub.com/apis/iOKids/Friends/1.0.0) |
| Application User Data | app/v1 <br/> app/v1/data <br/> app/v1/bucket <br> app/ws (websockets) | Application-specific User Data API | [swagger doc](https://app.swaggerhub.com/apis/iOKids/ApplicationUserData/1.0.0) |
| Images | image/v1/static | Image API | coming soon |
| Search | user/v1/search <br/> user/v1/search/random | Search API | [swagger doc](https://app.swaggerhub.com/apis/iOKids/Search/1.0.0) |

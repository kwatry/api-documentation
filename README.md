# playPORTAL API Documentation

## Overview
Want to build a kids or family focused app or smart toy? Using the playPORTAL APIs, you can add personalized and social 
features into your apps, achieving easy child privacy compliance with [COPPA](https://www.ftc.gov/enforcement/rules/rulemaking-regulatory-reform-proceedings/childrens-online-privacy-protection-rule)
 and GDPR. 

playPORTAL provides a single interface app where your users, even kids under 13, build up their friends lists and parents 
can control who and what their kids can do through the platform. Using the playPORTAL secure API, you can easily integrate 
our kid-safe [social sign on](/playPORTAL-SSO.md) (login) to allow for kid-safe user customization, multi-player modes, 
battle-modes, realtime competitions, chat, and communities just to name a few.

The [playPORTAL app](https://iokids.net/pages/download-iokids) is the command center for the playPORTAL platform. Here you can 
launch Communities and Character pages to engage current users and allow new users to discover your brand through videos 
and Magic Messages. Your Communities link directly with your interactive apps and games deployed on the platform 
providing full 360-degree engagement. 

What are you waiting for? Let’s start creating cool connected play experiences today! Welcome to the playPORTAL platform!

## Getting Started
1. [Sign-up](https://partner.iokids.net) to be an playPORTAL Partner. Review our <a href="playPORTAL-Developer-Setup.pdf" download>Step 
by Step guide</a> for developer on-boarding.
2. Log-in to the [partner dashboard](https://partner.iokids.net/) to [create an application](/CreateAnApplication.md) 
that will interact with the playPORTAL APIs. You will need an application identifier to use any of the playPORTAL APIs.
3. Start you application by integrating the playPORTAL Social Sign On. Start by reading the 
[API documentation](/playPORTAL-SSO.md). Follow our examples and integrate within an hour.
4. Socially enable your app by integrating with any of the APIs above. Test your integration in our sandbox environment 
(download our <a href="playPORTAL-APIs.postman_collection.json" download>Postman test suite</a> and 
<a href="playPORTAL-APIs.postman_environment.json">environment variables</a> to run a test of each API). 
5. Upgrade your account to become an [playPORTAL Partner](https://iokids.net/partners) and go live!

## Resources

1. You will create applications and users in the [partner dashboard](https://partner.iokids.net/).
2. Learn how to use the partner dashboard for sandbox testing with our <a href="playPORTAL-Developer-Setup.pdf" download>developer set-up guide</a>.
3. Download and use this <a href="playPORTAL-APIs.postman_collection.json" download>Postman collection</a> and 
<a href="playPORTAL-APIs.postman_environment.json" download>environment variables</a> to see example calls. 
4. Learn how to configure the Postman collection and environment variables with our 
<a href="Configure-Postman-for-playPORTAL.pdf" download>configuration guide</a>.

## Which APIs do I Need?
Every developer must implement the [playPORTAL Social Sign-On API](/playPORTAL-SSO.md). Most developers will will want to interface
with the [User Profile](https://app.swaggerhub.com/apis/playPORTAL/Profile/1.0.0) and [Friends](https://app.swaggerhub.com/apis/playPORTAL/Friends/1.0.0) APIs. Other APIs are available for various needs: 
inviting friends to use interactive games, securely storing user data your app needs, interfacing with other applications 
and toys, and managing the permissions that govern all of these interactions. For detailed documentation about each API, 
click the name below. 

| API | Version | Release Status | Description |
| --- | ------- | ------ | ----------- |
| [playPORTAL <br />Social Sign On](/playPORTAL-SSO.md) | 1.0.0 | released | Integrate playPORTAL users with your application. |
| [Profile](https://app.swaggerhub.com/apis/playPORTAL/Profile/1.0.0) | 1.0.0 | released | Retrieve profile information about an playPORTAL user |
| [Friends](https://app.swaggerhub.com/apis/playPORTAL/Friends/1.0.0) | 1.0.0 | released | Get a users' list of friends, establish new friendships through your app |
| [Search](/https://app.swaggerhub.com/apis/playPORTAL/Search/1.0.0) | 1.0.0 | released | Search for other playPORTAL users who use your application |
| [Application User Data](/ApplicationData.md) | 1.0.0 | released | Securely store the user data your app needs |
| [Image](https://app.swaggerhub.com/apis/playPORTAL/Image/1.0.0) | 1.0.0 | released | Retrieve and store images |
| Notify | 1.0.0 | pre-release | Update other users of your application as needed to support realtime competitions |
| Share to playPORTAL |  | *planning* | Share content from your app or toy on an playPORTAL profile and with friends |
| Chat |   | *planning* | COPPA-compliant chat between friends **with moderation** |
| Invite |  | *planning* | Invite others to engage through your app |
| Applications and Toys |  | *planning* | Get a users' list of applications and the interactions they offer |
| Permissions |  | *planning* | Manage user permissions for application use, features enablement, and shareability |
| MojiTalk<sup>TM</sup> |  | *planning* | Text to speech messages with Emoji Sounds |
| Internet of Toys<sup>&reg;</sup> |  | *planning* | Allow toys and kids' devices to safely connect wirelessly with each other and cloud driven content. Discover other toys on the network and use electronic toys for control and environmental monitoring. |



# Internet of Kids<sup>TM</sup> (iOKids) API Documentation

## Overview
Want to build a kids or family focused app or smart toy? Using the iOKids APIs, you can add personalized and social 
features into your apps, achieving easy child privacy compliance with [COPPA](https://www.ftc.gov/enforcement/rules/rulemaking-regulatory-reform-proceedings/childrens-online-privacy-protection-rule)
 and GDPR. 

iOKids provides a single interface app where your users, even kids under 13, build up their friends lists and parents 
can control who and what their kids can do through the platform. Using the iOKids secure API, you can easily integrate 
our kid-safe [social sign on](/iOKids-SSO.md) (login) to allow for kid-safe user customization, multi-player modes, 
battle-modes, realtime competitions, chat, and communities just to name a few.

The [iOKids app](https://iokids.net/pages/download-iokids) is the command center for the iOKids platform. Here you can 
launch Communities and Character pages to engage current users and allow new users to discover your brand through videos 
and Magic Messages. Your Communities link directly with your interactive apps and games deployed on the platform 
providing full 360-degree engagement. 

What are you waiting for? Let’s start creating cool connected play experiences today! Welcome to the iOKids platform!

## Which APIs do I Need?
Every developer must implement the [iOKids Social Sign-On API](/iOKids-SSO.md). Most developers will will want to interface
with the [User Profile](/Profile.md) and [Friends](/Friends.md) APIs. Other APIs are available for various needs: 
inviting friends to use interactive games, securely storing user data your app needs, interfacing with other applications 
and toys, and managing the permissions that govern all of these interactions. For detailed documentation about each API, 
click the name below. 

| API | Version | Release Status | Description |
| --- | ------- | ------ | ----------- |
| [iOKids <br />Social Sign On](/iOKids-SSO.md) | 1.0.0 | released | Integrate iOKids users with your application. |
| [Profile](/Profile.md) | 1.0.0 | released | Retrieve profile information about an iOKids user |
| [Friends](/Friends.md) | 1.0.0 | released | Get a users' list of friends, establish new friendships through your app |
| [Invite](/Invite.md) | 1.0.0 | *planning* | Invite others to engage through your app |
| [Application User Data](/ApplicationData.md) | 1.0.0 | released | Securely store the user data your app needs |
| [Notify](Notify.md) | 1.0.0 | released | Update other users of your application as needed to support realtime competitions |
| Chat |   | *planning* | COPPA-compliant chat between friends **with moderation** |
| Applications and Toys |  | *planning* | Get a users' list of applications and the interactions they offer |
| Share to iOKids |  | *planning* | Share content from your app or toy on an iOKids profile and with friends |
| Permissions |  | *planning* | Manage user permissions for application use, features enablement, and shareability |
| MojiTalk<sup>TM</sup> |  | *planning* | Text to speech messages with Emoji Sounds |
| Internet of Toys<sup>&reg;</sup> |  | *planning* | Allow toys and kids' devices to safely connect wirelessly with each other and cloud driven content. Discover other toys on the network and use electronic toys for control and environmental monitoring. |

## Getting Started
1. Sign-up to be an iOKids Partner (contact us!)
2. Log-in to the [partner dashboard](https://partner.iokids.net/) to [create an application](/CreateAnApplication.md) 
that will interact with the iOKids APIs. You will need an application identifier to use any of the iOKids APIs.
3. Start you application by integrating the iOKids Social Sign On. Start by reading the 
[API documentation](/iOKids-SSO.md). Follow our examples and integrate within an hour.
4. Socially enable your app by integrating with any of the APIs above. Test your integration in our sandbox environment 
(download our Postman test suite to run a test of each API).
5. Upgrade your account to become an [iOKids Partner](https://iokids.net/partners) and go live!

## Resources

1. You will create applications and users in the [partner dashboard](https://partner.iokids.net/).
2. Download and use this <a href="iOKids-APIs.postman_collection.json" download>Postman collection</a> and <a href="iOKids-APIs.postman_environment.json">environment variables</a> to see example calls. You will need to configure
the collection for your sample user.


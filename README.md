# Internet of Kids<sup>TM</sup> (iOKids) API Documentation

## Overview
The iOKids platform offers **[COPPA compliant](https://www.ftc.gov/enforcement/rules/rulemaking-regulatory-reform-proceedings/childrens-online-privacy-protection-rule)** 
APIs that developers use to legally enable their products for use by children younger than 13 years old. 

Using the iOKids APIs, you **inherit verifiable parental consent so children can use your products**. iOKids manage your 
privacy policy and communicate to parents the kind of information your application collects, stores, and shares. 
Finally, it offers developers a way to integrate our kid-safe social network into web and mobile apps so that you can 
build a COPPA compliant community around your product. 

With iOKids, your users can share content, games, applications, pictures and video with friends and family. Children can 
play interactive games with friends and even connect with physical toys. 

## Which APIs do I Need?
Every developer must implement the [iOKids Social Sign-On API](/iOKids-SSO.md). Most developers will will want to interface
with the [User Profile](/Profile.md). Other APIs are available for various needs: retrieving and managing friends, 
challenging friends to interactive games and tracking results, interfacing with other applications and toys, and managing
the permissions that govern all of these interactions. For detailed documentation about each API, click the name below. 

| API | Version | Release Status | Description |
| --- | ------- | ------ | ----------- |
| [iOKids <br />Social Sign On](/iOKids-SSO.md) | 1.0.0 | released | Integrate iOKids users with your application. |
| [Profile](/Profile.md) | 1.0.0 | released | Retrieve profile information about an iOKids user |
| Friends |  | *planning* | Get a users' list of friends, establish new friendships through your app |
| MojiTalk |  | *planning* | Text to speech messages with Emoji Sounds |
| Share to iOKids |  | *planning* | Share content from your app or toy on an iOKids profile and with friends |
| Challenge |  | *planning* | Allow users to challenge friends to play your app and track statistics |
| Chat |   | *planning* | COPPA-compliant chat between friends **with moderation** |
| Applications and Toys |  | *planning* | Get a users' list of applications and the interactions they offer |
| Permissions |  | *planning* | Manage user permissions for application use, features enablement, and shareability |
| Internet of Toys |  | *planning* | Allow toys and kids' devices to safely connect wirelessly with each other and cloud driven content. Discover other toys on the network and use electronic toys for control and environmental monitoring. |

## Getting Started
1. All applications must integrate iOKids Social Sign On. Start by reading the [API documentation](/iOKids-SSO.md). Follow 
our examples and integrate within an hour.
2. Set-up an account in the [Developer Sandbox](https://sandbox.iokids.net/developer) and register your application in 
the developer's portal.  
3. Integrate the [iOKids Social Sign-On](/iOKids-SSO.md) API and any of the others shown above.
4. Test your integration in our test environment.
5. Upgrade your account to become an [iOKids Partner](https://iokids.net/partners) and go live!


APIs and Documentation - Copyright 2017, Dynepic Inc. - All rights reserved
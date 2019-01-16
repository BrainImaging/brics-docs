
# User Management
The User tab allows the creation, editing, and management of Users.

## Authentication
BrICS can currently use two types of authentication - Shibboleth or the Auth0 service. Shibboleth allows one to login via single-sign on (SSO) using their institutional (e.g. Emory NetID) credentials. [Auth0](https://auth0.com) is a third party service that also allows SSO using a variety of providers, such as Google, GitHub, Microsoft, etc. There is a slight difference in how users are setup from each, so we'll include info on both below.
Currently, the main BrICS installation at https://brics.me utilizes Auth0 with sign-in through Google; if a different provider is selected, the instructions below may need to be adjusted.
## Creating a New User

From the User Management view, click **Create New**. A template will load. All fields with asterisks are required to be filled out.
### username
The username for this user. When using Shibboleth at Emory, this will be user's NetID. When using Auth0 (default), this will be the [local-part](https://en.wikipedia.org/wiki/Email_address#Local-part) of the user's email address. For example, if I login with coolbricsuser101@gmail.com, my username would be **coolbricsuser101**.
### email
The user's email address.
### display_name
What the user will be displayed as in BrICS. Often, we'll use a full name with credentials (e.g. Hyunsuk Shim, PhD) for our s
> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyNDA0NTM3MSwxMTM4Njg0MTcwXX0=
-->

# User Management
The User tab allows the creation, editing, and management of Users.

## Authentication
BrICS can currently use two types of authentication - Shibboleth or the Auth0 service. Shibboleth allows one to login via single-sign on (SSO) using their institutional (e.g. Emory NetID) credentials. [Auth0](https://auth0.com) is a third party service that also allows SSO using a variety of providers, such as Google, GitHub, Microsoft, etc. There is a slight difference in how users are setup from each, so we'll include info on both below.

Currently, the main BrICS installation at https://brics.me utilizes Auth0 with sign-in through Google; if a different provider is selected, the instructions below may need to be adjusted.
## Creating a New User

From the User Management view, click **Create New**. A template will load. All fields with asterisks are required to be filled out.

![enter image description here](https://i.imgur.com/g7xecEA.png)

### username
The username for this user. When using Shibboleth at Emory, this will be user's NetID. When using Auth0 (default), this will be the [local-part](https://en.wikipedia.org/wiki/Email_address#Local-part) of the user's email address. For example, if I login with coolbricsuser101@gmail.com, my username would be `coolbricsuser101`.

### email
The user's email address.

### display_name

What the user will be displayed as in BrICS. Often, we'll use a full name with credentials (e.g. Hyunsuk Shim, PhD) for our clinical studies.
### administrator

A field that specifies whether the user should be a BrICS administrator. By default, this should be set to **False**; for developers and project leads, this should be set to **True**.

### project_list
This field is a list of projects the user should have access to. Select **Add Item** for each project the user should have access to. For each project, you will need to type in the **project_id** (see [Project Management](../project/) for more info on this field). If you start typing in a project_id, an autocomplete field will popup.

![enter image description here](https://i.imgur.com/23lovHm.png)

## Editing Users

You can edit an existing user by selecting it from the drop-down menu in the User Management view.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ4MTI5NTI0Nl19
-->
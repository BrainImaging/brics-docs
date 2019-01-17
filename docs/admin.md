# Admin Module

This portion of the guide will show you how to use the Admin module to set up projects, users, and manage other settings for BrICS.

## Accessing the Admin Module
In order to access the Admin Module, your account must be an administrator within BrICS. If you are not an administrator, you will need to ask one of the administrators to add you.
> **Note**: if you're running a local version of BrICS, e.g. within a Docker container, by default no authentication is setup, and you are automatically logged in as an administrator.

Once you've logged in to BrICS, open up the left side bar by clicking the menu icon on the top right of the screen. If you're logged in as an administrator, a button labeled **Admin** will be available.

![enter image description here](https://i.imgur.com/kbKAslH.png)

You will then be taken to the Admin Module.

![enter image description here](https://i.imgur.com/Fh4rbAI.png)

## Admin Module Components
The Admin module has four basic views, which can be accessed from the top menu bar. We will go through each of these on its own page.

 - [Project Management](project)
 - [User Management](../admin/user)
 - [Environmental Variables](../admin/environment)
 - [Unit Testing](../admin/unit-test)

# Project Management

The Projects tab allows the creation of new BrICS projects and editing of existing ones. Let's start by creating a new project, and then walking through how to set it up.

## Create a New Project
Make sure you are on the Projects tab. Then, click **Create New**. A template for a new project will then load.
![enter image description here](https://i.imgur.com/jpkMCPn.png)	

All fields with an asterisk need to be filled out, though in general it is good to fill out all fields as needed. We will go through each of them one by one below.

### proj_id
The proj_id represents the ID for this project. It is an **alphanumeric** string (no spaces or special characters) that will be used internally to manage all data for this project. You can set it to something memorable (e.g. test_project_jan2019) or something random. Once set, it *cannot be changed*. 

### name
The name for the project. This can be any string, and it is useful to make this a quick descriptor of the project. For example, if I were making a project consisting of sMRI scans for grade II glioma biopsies, I might name it "Grade II Biosies"

### metabolites
This field consists of a list of metabolites we want to use in this project. It can be edited later, but it's good to set up a few for the time being. Start by click **Add Item** to enter your first metabolite, and repeat for all additional ones you want. Each metabolite has three fields:
 

 - **id**: this is the MIDAS ID for the metabolite. For example, the water-normalized choline map is called **tCholine**, while the Cho/NAA ratio map is called **CHO/NAA**. A quick way to check this is to look through a sample study in MIDAS and determine what metabolite frames are presentd.
 - **name**: This is what the metabolite should be called when displayed in BrICS. It can be whatever you'd like, since this field is  only for display purposes.
 - **IU**: For all non-ratio images, this is used to determine how the metabolite maps are scaled on display. In sMRI scans, the actual voxel values for a metabolite have no inherent calibration, and are thus given units of "Institutional Units." These enable comparison within and across subjects, but have not been calibrated to actual concentrations. 
The value given here will be the maximum value used for display, i.e. the metabolite will be scaled from 0 to the specified value. A common starting point is 10000 for most metabolites, and can be adjusted as needed to produce well-scaled images.
Ratio images,, for obvious reasons, do not need a value for this field.

### location
**Don't set this field manually**. It will be automatically determined once you save the project.

### midas_autoscan
If you want this BrICS project to be tied to a MIDAS project (which, in most cases, you do), then specify the location of the project here. Remember, **the location of the project must be from the context of the BrICS server**; BrICS does not have access to your local hardrive. A good way to have a project that can be both edited using MIDAS on your local computer and visible to BrICS is to put it on a shared drive accessible by both machines. 

Double-lick on the field to open up a server-side file browser. Our laboratory's shared drive (the so-called **ShimLab Array** or Synology Array) is already mounted on BrICS server under `/array`, so you can access projects from within there.

![enter image description here](https://i.imgur.com/Da2I24F.png)

Find the folder for the MIDAS project. This must be the folder where the project.xml file is located. Then click **Open**.

### invert_spectrum
This field indicates whether all the spectra in this project are inverted (i.e. upside-down). This occurs on some scanners / sequences  when there is a 180 degree phase shift. MIDAS will usually fix this during its phase-correction, and so for most projects, select **False** for this field. However, for projects where the spectra do appear upside-down, select **True**.

### autonorm
This field indicates whether or not the Gaussian Mixture Model autonormalization algorithm (see Gurbani et. al., *Tomography* 2019) for ratio images. In most cases, you want this to be set to **True**.

### redcap
This set of fields allows this BrICS project to be connected to a REDCap database for pulling in subject metadata.

 - **api_url**: The API URL for the REDCap database. Please check the REDCap database's documentation for what URL to put here. It needs to end with a forward slash (`/`).
 - **api_token**: An alphanumeric string that is your authentication token to access REDCap. You will need to contact your REDCap administrator to get this token.
 - **subject_variable**: This is the ID of the variable in REDCap that corresponds to subject ID. Depending on how REDCap is set up, this may be called various things such as **subject_id**, **study_id**, etc. This is necessary, as it allows BrICS to search for a specific subject in REDCap.
> NOTE: Do **NOT** use any field that contains PHI for the subject_ variable. BrICS is not HIPAA compliant and this should only query based on a de-identified subject ID.
 - **variables**: A list of variables that you want to pull from REDCap to display in BrICS. Click **Add Item** and fill out the two fields for each variable you want to pull.
 -- **label**: What you'd like the variable to be displayed as in BrICS
 -- **variable_name**: The name of the variable in REDCap.
 > NOTE: Again, as this is critically important: do **NOT** attach any variables that contain PHI. There is a setting in REDCap that will only allow your API token to access non-PHI fields; this should be set as such. However, if not, double check and make sure no PHI fields are input as variables here.

Once all these fields have been set, click the green **Add** button to add this project to BrICS. If there are any errors, you will be alerted.

## Editing an Existing Project
You can edit an existing project by selecting it from the drop-down menu in the Project Management view. Some fields, such as proj_id, cannot be edited after initial creation; however, most fields can, and the changes you make will immediately be available in BrICS.

## Next Steps

Once a project has been created (or edited), you will want to assign which Users should have access to it. Go to [User Management](../user/).


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

# Environmental Variables
BrICS consists of many different components. One of the core components is a C++ extension to PHP, named **libbrics**, that enables much of the image processing and spectral processing functions used by the app. Since libbrics needs to be compiled to binary code whenever changes are made to the C++ source files, we need a way to pass certain variables dynamically to it. For this, we use a special collection within our MongoDB database that libbrics can access. This collection can be modified in real-time using the Environmental Variables view in BrICS Admin.

![enter image description here](https://i.imgur.com/X2SJfIY.png)

Each variable has two fields:

 - **name**: the variable name. This is what libbrics will use to find the value. Some  existing variables include *skull_stripper_atlas_image_file* and *skull_stripper_atlas_mask_file*, which are used to identify files that are needed for the Skull Stripper algorithm.
 - **value**: the value that the variable will evaluate to when called in libbrics. This  will always be processed as a string (i.e. you cannot put scripting or code in here). For variables that need a filepath, double click on this field to bring up the server-side file browser. Otherwise, any string is fine.

# Unit Testing
The Unit Testing view enables quick testing of many of the components of BrICS. It is composed of [unit tests](https://en.wikipedia.org/wiki/Unit_testing) - individual scripts that assess whether a specific function of BrICS is working. These can be developed for things like connectivity checks, algorithms, and connections between modules.

Unit tests are stored in the main BrICS repository under `html/admin/tests`. 

This view allows you to quickly run either specific tests, a specific category of tests, or all tests.

![enter image description here](https://i.imgur.com/jVQ5JmL.png)
## Running a Test
To run a single test, click the **Run** button next to a test. The server will kick off the test and update when the test completes or errors out.

To run all tests within a category, click the **Run All** button for that category.

> **Note**: The first time a test is run, it will be in the "Uncategorized" category. Once it successfully completes, it will go into it's specified category.

To run all tests, scroll to the bottom of the page and click the blue button labeled **RUN ALL TESTS**.
> **Note**: Running all tests can take a long time, and will lock up the BrICS server while these are running. This is important to run if there have been major changes made to the code base, and should be run when others are not expecting to use the app.
> 
## Assessing Test Results
Once a test is run, it will return one of three possible outcomes.

### Passed
The test completed and returned a successful outcome. If there are any success messages from the test, they will be displayed (i.e. "the test received the expected outcome of xxxx").

![enter image description here](https://i.imgur.com/fnPMZgT.png)

## Error
The test completed, but the outcome was not as expected. The response message will give insight as to what the issue is. For example, in the image below, the test which tries to connect to Emory's REDCap database failed because the API credentials in the test script were incorrect.

![enter image description here](https://i.imgur.com/3OBk87p.png)

## Script Error
There was an error in the test script itself, and so the test could not be completed. This requires debugging of the test script and to remove any elements that could be causing a fatal error that prevents the script crom completing.

![enter image description here](https://i.imgur.com/WrsFVTX.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDM4OTg1NTddfQ==
-->
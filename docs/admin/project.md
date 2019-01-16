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

 - **api_url**: The API URL for the REDCap database. Please check the REDCap database's documentation for what URL to put here. It needs to end with a forward slash (**/**).
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

Once a project has been created (or edited), you will want to assign which Users should have access to it. Go to User Management.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MzU0MjU4MzFdfQ==
-->
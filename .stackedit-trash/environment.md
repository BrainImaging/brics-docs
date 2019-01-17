# Environmental Variables
BrICS consists of many different components. One of the core components is a C++ extension to PHP, named **libbrics**, that enables much of the image processing and spectral processing functions used by the app. Since libbrics needs to be compiled to binary code whenever changes are made to the C++ source files, we need a way to pass certain variables dynamically to it. For this, we use a special collection within our MongoDB database that libbrics can access. This collection can be modified in real-time using the Environmental Variables view in BrICS Admin.

![enter image description here](https://i.imgur.com/X2SJfIY.png)

Each variable has two fields:

 - **name**: the variable name. This is what libbrics will use to find the value. Some  existing variables include *skull_stripper_atlas_image_file* and *skull_stripper_atlas_mask_file*, which are used to identify files that are needed for the Skull Stripper algorithm.
 - **value**: the value that the variable will evaluate to when called in libbrics. This  will always be processed as a string (i.e. you cannot put scripting or code in here). For variables that need a filepath, double click on this field to bring up the server-side file browser. Otherwise, any string is fine.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3NzA2ODI1Ml19
-->
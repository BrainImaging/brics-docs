# Environmental Variables
BrICS consists of many different components. One of the core components is a C++ extension to PHP, named **libbrics**, that enables much of the image processing and spectral processing functions used by the app. Since libbrics needs to be compiled to binary code whenever changes are made to the C++ source files, we need a way to pass certain variables dynamically to it. For this, we use a special collection within our MongoDB database that libbrics can access. This collection can be modified in real-time using the Environmental Variables view in BrICS Admin.

![enter image description here](https://i.imgur.com/X2SJfIY.png)

Each variable has two fields:

 - **name**: the variable name. This is what libbrics will use to find the value. Some  existing variables include *skull_st

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMwODc5MTEwMF19
-->
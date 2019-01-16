# Environmental Variables
BrICS consists of many different components. One of the core components is a C++ extension to PHP, named **libbrics**, that enables much of the image processing and spectral processing functions used by the app. Since libbrics needs to be compiled to binary code whenever changes are made to the C++ source files, we need a way to pass certain variables dynamically to it. For this, we use a special collection within our MongoDB database that libbrics can access. This collection can be modified in real-time using the Environmental Variables view in BrICS Admin.

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDUxNjIzNDIxXX0=
-->
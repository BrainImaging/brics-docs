# Environmental Variables
BrICS consists of many different components. One of the core components is a C++ extension to PHP, named **libbrics**, that enables much of the image processing and spectral processing functions used by the app. Since libbrics needs to be compiled to binary code whenever changes are made to the C++ source files, we need a way to pass certain variables dynamically to it. For this, we use a special collection within our MongoDB database that the c
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1MzEzNDA2Nl19
-->
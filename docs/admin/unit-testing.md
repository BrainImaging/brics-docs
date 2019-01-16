# Unit Testing
The Unit Testing view enables quick testing of many of the components of BrICS. It is composed of [unit tests](https://en.wikipedia.org/wiki/Unit_testing) - individual scripts that assess whether a specific function of BrICS is working. These can be developed for things like connectivity checks, algorithms, and connections between modules.

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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1NjI3NjIxM119
-->
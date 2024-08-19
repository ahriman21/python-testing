### what is automated testing
Automated testing means writing codes to test your application's codes. It can be unit testing, integration testing, end-to-end testing.


### what is unit testing?
Unit testing means to test the sections/units of your application. in other words, unit testing is to break your app to small parts and test those small parts seperately.


### automated testing in python
How to write automatic tests in python? you can use some famous libraries to write tests for your application. libraries like `pytest`, `unittest`, or even using the docs to write test which is called `doctest`.


### some global principals that need to be copmpied:
- name of a class must start or end with the word of `test`.

-  name of a function must start with `test_` or end with `_test`

- to have a refactored code helps writing better unit tests.

- remember to test all functionalities of a unit. test for the behavior, implementation, security of the unit. for example if it is a api that adds data to database check if it is return the 200 response or check if the data is added to the data base in a correct way, or you can check the validity of data that user entered.


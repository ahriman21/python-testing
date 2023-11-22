# pytest tutorial
> by using this library we can create our test files in more flexible way. we don't have to inherit from any class to automate testing.  
> Running pytest without mentioning a filename will run all files of format test_*.py or *_test.py in the current directory and subdirectories.  
> to install pytest use this command :
```
pip install pytest
```

## implementting a test usng pytest
```python
import math

def test_sqrt():
   num = 25
   assert math.sqrt(num) == 5
```

## Run the test using the following command
```
pytest
```

## command below runs the test verbosity
```
pytest -v
```

## To execute the tests from a specific file, use the following syntax
```
pytest filename -v

```

## To execute the tests containing a string in its name we can use the following syntax
```
pytest -k substring -v
```
> example:  
> pytest -k great -v  
> This will execute all the test names having the word ‘great’ in its name. In this case, they are test_greater() and test_greater_equal(). See the result below.  

## grouping tests
> you can group some test functions to gether , then you can use a command to run only a group of test functions
> you can use `@pytest.mark.group_name` at the top of each function.  
> example :  
```
import pytest
import math

@pytest.mark.square
def test_sqrt():
   num = 25
   assert math.sqrt(num) == 5

@pytest.mark.square
def testsquare():
   num = 7
   assert 7*7 == 40

@pytest.mark.others
   def test_equality():
   assert 10 == 11
```
> to run a group of tests:
```
pytest -m markername -v

```

## fixtures
> Fixtures are functions, which will run before each test function.  
> Therefore, instead of running the same code for every test, we can attach fixture function to the tests and it will run and return the data to the test before executing each test.
> example :
```python
import pytest

@pytest.fixture
def input_value():
   input = 39
   return input

def test_divisible_by_3(input_value):
   assert input_value % 3 == 0

def test_divisible_by_6(input_value):
   assert input_value % 6 == 0

```


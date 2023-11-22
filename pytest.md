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

## conftest.py
> We can define the fixture functions in this file to make them accessible across multiple test files.
> create a file named conftest.py
> put your fixtures in it. then you can access your fixtures in another test files.


## parameterizing
> Parameterizing of a test is done to run the test against multiple sets of inputs. We can do this by using the following marker  

```
@pytest.mark.parametrize
```
> example:  
```python
import pytest

@pytest.mark.parametrize("num, output",[(1,11),(2,22),(3,35),(4,44)])
def test_multiplication_11(num, output):
   assert 11*num == output

```
> Here the test multiplies an input with 11 and compares the result with the expected output. The test has 4 sets of inputs, each has 2 values – one is the number to be multiplied with 11 and the other is the expected result.


## assert errors
> sometimes we want to test if a code will raise a particular error or not.
> for instance, we have a code that checks if user's age is under 18 or not, if it is then it raises a ValueError including a message. so we can test this code using `with` cluase in pytest:
```python
def age_check(age):
   if age < 18:
      raise ValueError(" age cannot be less than 18")
```
> now we can test code above :
```python

def test_age_check_invalid_input():
   with pytest.raises(ValueError):
      age_check(17)

```
> code above tests that the original function will raise an ValueError or not. in this case if the result be true, it means the original function will raise the error and the code is ok.


>  

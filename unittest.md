# Guide to Unit Tests in Python
> The unittest module is a framework designed to make our lives easier when it comes to testing code. The module works based on some important object-oriented concepts.  
> Methods of TestCase class in unittest module :    
assertEqual(a, b)          --------------->        a == b  
assertNotEqual(a, b)       --------------->        a != b  
assertTrue(x)	             --------------->        bool(x) is True  
assertFalse(x)	           --------------->        bool(x) is False  
assertIs(a, b)	           --------------->        a is b  
assertIsNot(a, b)	         --------------->        a is not b  
assertIsNone(x)	           --------------->        x is None  
assertIsNotNone(x)	       --------------->        x is not None  
assertIn(a, b)	           --------------->        a in b  
assertNotIn(a, b)	         --------------->        a not in b  
assertIsInstance(a, b)     --------------->	      isinstance(a, b)  
assertNotIsInstance(a, b)	 --------------->       not isinstance(a, b)

> note : It's important to say that all assert methods in the TestCase class also take a msg argument that is used as an error message in case the test fails.


## Implementing Unit Tests
> to implement our unittest, first we should have written our code :
```python
  # project/code/my_calculations.py

class Calculations:
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def get_sum(self):
        return self.a + self.b

```


> now it's time to implement test case:
```python
# project/test.py

import unittest
from code.my_calculations import Calculations

class TestCalculations(unittest.TestCase):

    def test_sum(self):
        calculation = Calculations(8, 2)
        self.assertEqual(calculation.get_sum(), 10, 'The sum is wrong.')

if __name__ == '__main__':
    unittest.main()

```

## how to run your test
```
python -m unittest -v file_name.py
```

## unittest fixtures
> The setUp Method : Now that we understand the basics of unit testing with the unittest module, let's optimize our code a bit. You probably have noticed that inside each test we initialized an object of the Calculations class, which will be tested. However, we can avoid that by creating a setUp method.
The TestCase class already has a setUp method that runs before each test. So what we'll do when creating a new one is actually overwrite the default method with our own. This is the code with this new method implemented:
```python
import unittest
from code.my_calculations import Calculations

class TestCalculations(unittest.TestCase):

    def setUp(self):
        self.calculation = Calculations(8, 2)

    def test_sum(self):
        self.assertEqual(self.calculation.get_sum(), 10, 'The sum is wrong.')

```

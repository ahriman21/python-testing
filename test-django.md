### provided test tools in django :
* SimpleTestCase : use it if your tests dont make any database query. this class disallows database queries by default
* TransactionTestCase : use it if your tests make any database query.
* TestCase : this is the most common class to use for writing tests in django. it inherits from both classes above.

all of these classes above inherit from `unittest.TestCase`. so it has all features of unittest module.

#### SimpleTestCase :
```python
from django.test import SimpleTestCase

class UserTestCase(SimpleTestCase):
  def test_email_validate(self):
    """ this test returns true if the statement in assertTrue is true."""
    self.assertTrue('@gmail.com' in 'x@gmail.com') # returns true

  def test_invalid_email(self):
    """ this test returns true if the statement in assertFalse is false."""
    self.assertFalse('@gmail.com' not in 'x@gmail.com')
```

#### how to run tests in django :
```shell
# run all tests in your projects
$ python manage.py test

# run all tests in users.tests module (users for example is the name of an app in a django project)
$ python manage.py test users.test

# run all the test found in users package
$ python manage.py test users

# run just one test case
$ python manage.py test users.tests.UserTestCase

# run just one method
$ python manage.py test users.tests.UserTestCase.test_invalid_email
```
note : `.` means the test returned ok and `F` means the test returned false.

#### tree structure of test files in django :
```
> ./project
  > ./app
    > ./tests
      > __init__.py
      > test_x.py
      > test_y.py
      > ...
```






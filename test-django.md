### provided test tools in django :
django has some classes to help us test projects. all of these classes inherit from `unittest.TestCase`. so it has all features of unittest module.
you can access them from `django.test`.
* SimpleTestCase : use it if your tests dont make any database query. this class disallows database queries by default
* TransactionTestCase : use it if your tests make any database query.
* TestCase : this is the most common class to use for writing tests in django. it inherits from both classes above.

note : django will create test database for your tests and dosn't use the database you are using for your production.



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


#### how to use data before running each methdod or class | setUpTestData() VS setUp()  :
if you want to use a data that repeats in your test methods again and again, you can put it in a method called `setUp` or `setUpTestData`.
once you write this method and put the data in it, you can use that in all of your test methods in the module.
* `setUp` method runs before each method.
* `setUpTestData` runs before a test class. this method is a class meethod and should use `@classmethod` decorator.

```python
class TestAuthor(TestCase):
  def setUp(self):
    self.author = baker.make(Author, name='bob', nation='german')

  def test_author_instance_str(self):
    """ test if the __str__ method in Autho model is working well or not """
    self.assertEqual(str(self.author), 'bob')
```

#### how to use fake data in test files | model_bakery :
you can use fake data in your database using model_bakery package
```python
from model_bakery import baker
from authors.models import Author

# create a fully random author object
author = baker.make(Author)

# you can pass some of data yourself
author2 = baker.make(Author, name='kevin')
```

#### example of how to test form classes of an object :
in this example the model is User and the form class is UserRegisterForm
```python
from django.test import TestCase
from users.models import User
from users.forms import UserRegisterForm

class TestUserRegistrationForm(TestCase):
  def test_valid_sata(self):
    """ this method tests the result of entering valid data into UserRegisterForm class"""
    form = UserRegisterForm(data={'username':'bob', 'email':'x@gmail.com'})
    self.assertTrue(form.is_valid())

  def test_empty_form(self):
    """ this method tests the result of entering empty data """
    form = UserRegisterForm(data{})
    self.assertFalse(form.is_valid())
    self.assertEqual(len(form.errors), 2)

  def test_email_existance(self):
    """ if you have a method that checks duplicate emails in your User model,
        you can use this method to test that method and insure that nobody can enter duplicate email
    """
    User.objects.create_user(username='kevin', email='kevin@kevin.com')
    form = UserRegisterForm(data={'username':'bob', 'email':'kevin.@kevin.com''})
    self.assertTrue(form.has_error('email'))
  

```

#### how to test views as a real client | client :
you can test your views like a real client is requesting your website and views. for that we import Client from django.test.
we can login, send data, send request and ... using `Client`.

* test a request to a url(GET,POST), test if login and accessing a permission needed view is working ok or not :
```python
from django.test import TestCase, Client

class TestUserRegisterView(TestCase):
  def setUp(self):
    self.client = Client()

  def test_user_register_GET(self):
    """ test the GET request to user registration view """
    respone = self.client.get(reverse('users:register'))
    self.assertEqual(response.status_code, 200) # test the status code
    self.assertTemplateUsed(response, 'users/register.html') # check if the response returns the correct template
    self.failUnless(response.context, UserRegisterForm) # check if the response returns the correct form

  def test_user_register_POST(self):
    """ test the POST request to user registration view """
    response = self.client.post(reverse('users:user-register'), data={'username':'bob', 'email':'bob@gmail.com', 'pass1':'pass', 'pass2':'pass'})
    self.assertRedirects(response, reserve('users:login')) # test if after submiting form it redirects us to login page or not
    self.failIf(response.context['form'].is_valid() == False) # test if form.is_valid() returns false
    self.assertFormError(form=response.context['form'], field='email', errors=['the email is already exists!']) # test if email field returns error or not

  def test_limited_view(self):
    """ this method tests a view that needs user to be authenticated before entering this view """
    User.objects.create_user(username="bob", email="bob@bob.com", password="1234", country="italy")
    self.client.login(email="bob@bob.com", password="1234")
    response = self.client.get(reverse('userrs:profile'))
    self.assertEqual(response.status_code, 200)
    self.assertTemplateUsed(response, 'users/profile.html')
    
```









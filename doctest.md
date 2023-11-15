### Doctest
>  doctest is a way to write tests for your python codes. you can use it to test your classes, methods, functions and more.
to write doctest tests you can use embedded codes in docstrings.
> doctest includes two sections :
> 1-your codes that must be written after '>>>' sign.
> 2-the result that you expect to be displayed in the next line.

> you can run your test via the following code:
> python -m doctest -v your_file_name.py
```
def sum(x,y):
  """
    >>> sum(4+5)
    9
  """
  return x + y
```

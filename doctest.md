### Doctest
>  doctest is a way to write tests for your python codes. you can use it to test your classes, methods, functions and more.
to write doctest tests you can use embedded codes in docstrings.
> doctest includes two sections :
> 1-your codes that must be written after '>>>' sign.
> 2-the result that you expect to be displayed in the next line.

> you can run your test via the following code:
> python -m doctest -v your_file_name.py
```python
def sum(x,y):
  """
    >>> sum(4+5)
    9
  """
  return x + y

```

> note : notice that if you have a string as your expecting result in docstrings, you have to wrap it with single quotes.


> you can also write your tests in '.md' files and call your .md file to run your test. to do this you should put your codes between triple backticks (```) . don't forget to leave a new line before the closing backticks.
> you can write your test codes in a simple '.txt' file like '.md' files. for instance :

```
>>> import calculations

>>> calculations.add(2, 2)
4.0

>>> calculations.subtract(2, 2)
0.0

>>> calculations.multiply(2, 2)
4.0

>>> calculations.divide(2, 2)
1.0
```

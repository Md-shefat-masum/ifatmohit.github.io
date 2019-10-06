---
layout: post
title: "Prettify your python class with Data Model Method"
author: "Mohidul Islam"
---

In python, there is some special built-in method called the data model method. They are very easy to recognize because they start and end with double underscores, for example, `__init__` or `__str__`.

As it is very tedious to say under-under-method-under-under Pythonistas adopted the term "dunder methods", a short term of **double underscore**.

These "special methods" are also sometimes called "magic method", but using this terminology can make them more complicated as they are. There is nothing magical about them. They are very straight forward. **They just allow you to emulate the behavior of the built-in types**.

In this tutorial, we will use various dunder methods in a Book class and make this class more Pythonic.

```python
class Book:
    pass    
```
A simple Book class nothing interesting in it. Let's make an object of this class.

```python
class Book:
    pass

b1 = Book()
b1.title = 'The Alchemist'
b1.author = 'Paulo Coelho'
b1.page = 208
b1.price = 25
```
If you are familiar with python class before you probably think why I wrote this in 5 lines while I could write it into one line. Instead of constructing my book and then initialize it I can construct and initialize them all together. So how do I do that? Well, I need an `__init__` method.

```python
class Book:
     def __init__(self, title, author, page, price):
        self.title = title
        self.author = author
        self.page = page
        self.price = price

b1 = Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)
```
Let run the code in interactive shell


```bash
~ python -i data-model.py
>>> b1
<__main__.Book object at 0x7fbc70a43978>
```

Oh my goodness what it printing out of the screen! It looks so ugly. It gives us a memory location. It isn't that good representation. I am here missing another method that corresponds to what happens when I call the function `repr(obj)` to figure out the representation of python objects. 
Let's implement that.

```python
class Book:
     def __init__(self, title, author, page, price):
        self.title = title
        self.author = author
        self.page = page
        self.price = price
   
    def __repr__(self):
        return f"Book(title='{self.title}', author='{self.author}', page={self.page}, price={self.price})"



b1 = Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)
```
```bash
~ python -i data-model.py
>>> b1
Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)

```
It looks a lot better.


In python, there is function call `len()` which gives you the size of an object. What would make sense for the size of a book? It probably is the number of pages. To implement it we have a `__len__()` method.


```python
class Book:
     def __init__(self, title, author, page, price):
        self.title = title
        self.author = author
        self.page = page
        self.price = price
   
    def __repr__(self):
        return f"Book(title='{self.title}', author='{self.author}', page={self.page}, price={self.price})"
    
    def __len__(self):
        return self.page


b1 = Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)
```
```bash
~ python -i data-model.py
>>> len(b1)
208
```

If we want to delete or remove an object from memory we use `del` keyword.
```bash
~ python -i data-model.py
>>> b1
Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)
>>> del b1
>>> b1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'b1' is not defined

```

 It just removes this object from memory saying nothing to us. What if it gives us a message like "The book has been deleted!". Well, we can do it by implementing the `__del__()` method.
```bash
>>> b1
Book(title='The Alchemist', author='Paulo Coelho', page=208, price=25)
>>> len(b1)
208
>>> del b1
The book has been deleted!
```


## There are even more dunder methods!
Showing each and every dunder method would make for a very long tutorial. If you want to learn more about dunder methods and the Python data model I recommend you go through the [Python reference documentation](https://docs.python.org/3/reference/datamodel.html).

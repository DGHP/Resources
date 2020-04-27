I'm going to focus on the ```from y import x``` syntax. There is also plain old ```import y```.

All my information comes from [this](https://realpython.com/absolute-vs-relative-python-imports/) article.

## The difference between modules and packages

- A Python __module__ is a file with a .py extension
- A Python __package__ is a folder with a collection of .py files inside it. Packages often contain ```__init__.py``` files. In Python 2 days, they had to. 

## What's valid on the left hand of from y import x ?

Either packages or modules. 

Python first looks for modules that have been previously imported in its cache of modules; next it (normally) looks in the local directory, and after that some other directories. The exact order of directories is defined in ```sys.path```.

For reference, inside my app I called

```
import sys
print(sys.path)
```

and got this:

```
['/home/ivo/personal-projects/flask-mega-tutorial', 
'/home/ivo/personal-projects/flask-mega-tutorial/venv/bin', 
'/usr/lib/python36.zip', 
'/usr/lib/python3.6', 
'/usr/lib/python3.6/lib-dynload', 
'/home/ivo/personal-projects/flask-mega-tutorial/venv/lib/python3.6/site-packages']
```

Exciting stuff. 

A final, but quite important, thing to note is that importing a package essentially imports its ```__init.py``` file.

## What's valid on the right-hand side of from y import x ?

- A module
- A subpackage
- An _object_, like a class or function

So basically anything.

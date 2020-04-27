# Python and Flask

 - [Introductions](#introductions)
   - [Introduction to Python](#introduction-to-python)
   - [Introduction to Flask](#introduction-to-flask)
   - [pip](#pip)
     - [A key difference between pip and npm](#a-key-difference-between-pip-and-npm)
 - [Things to know about Python syntax](#things-to-know-about-python-syntax)
 - [Accessing a MongoDB database in Python](#accessing-a-mongodb-database-in-python)
 - [Password authentication/login in Python](#password-authenticationlogin-in-python)
 - [Server and unit testing frameworks](#server-and-unit-testing-frameworks)
 - [Game logic written in Python](#game-logic-written-in-python)

## Introductions

### Introduction to Python

Python, as a language, needs to be installed on a computer (like Node). It doesn't run in the browser, like JavaScript does. Python scripts end with .py. Once Python is installed, you can run a python script with

  python example-script.py

although the command you use might change depending on how you've installed Python. 

Python 3 and Python 2 are incompatible. We should all try to use the same version of Python, using pyenv, a Python version manager like nvm (more forthcoming). When we deploy, we can tell Heroku/whatever to use that specific Python version.


### Introduction to Flask
flask is a framework, like Express. On the surface, at least, it's pretty similar:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

This program will, I think, respond to a get request to the home URL with the text 'Hello, World!', by calling the function hello_world()

### pip
pip is Python's standard package manager, like npm is for JavaScript. pip comes installed with Python 3.4 +, and has the same install syntax as npm, e.g.

```
pip install bcrypt
```

The Python equivalent of a package.json is a requirements.txt

You can make and maintain one using pip freeze:

```
pip freeze > requirements.txt
```

and then when installing a project on another machine, use

```
pip install -r requirements.txt
```

For dev dependencies, you use a different file called requirements_dev.txt. Inside this file, you call the requirements.txt file:

```
# In requirements_dev.txt # Python comments are hashes
-r requirements.txt
```

Then in development, you run pip install -r requirements_dev.txt and it also installs requirements.txt


There's a lot more you can do, of course. [Here's a link](https://realpython.com/what-is-pip/).

#### A key difference between pip and npm

npm installs packages in the project directory, unless you provide the -g flag to install globally. pip, meanwhile, installs packages globally. This is problematic when you are working on more than one project, because if both projects require the same package, but require different versions of the package, you're screwed. As a result, most people use a package called virtualenv which makes a local copy of your packages and your installation of Python(!) and runs python scripts from there instead of globally. 

virtualenv can be combined with pyenv, and there's even a program called pyenv-virtualenv which is designed to do exactly that. However if you want to use Python 3.3+ pyenv-virtualenv uses venv instead of virtualenv, which is a different program for doing the same job. Its all a bit of a mess, but here's [some instructions](https://gist.github.com/wronk/a902185f5f8ed018263d828e1027009b) at least.


## Things to know about Python syntax 

The biggest thing to know about Python syntax is that __whitespace matters__. Python doesn't have all the curly braces and brackets of a JavaScript program, and instead it uses indentation and whitespace for structure. The default Python tab is 4 spaces. 

Another difference from JavaScript is that variables are never declared (there is nothing like a let, var or const keyword), only assigned.

If you want to mainline some Python syntax, I recommend going here:

https://learnxinyminutes.com/docs/python/

A final thing to note about Python is that it supports OOP concepts like classes, inheritance and encapsulation in a way that JavaScript does not. If we implement the game logic in Python, we might want to do it with OOP, which is good for modelling tangible things like cards and players, but this will take some learning. 

## Accessing a MongoDB database in Python
I think that the best-documented approach will be PyMongo, which is maintained by the MongoDB team. Here is a link:

https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb

## Password authentication/login in Python

Python has a bcrypt package with a generally similar API to the JavaScript bcrypt package.

For JWTs we could use PyJWT.

## Server and unit testing frameworks
- pytest


## Game logic written in Python
 (another alternative is to write the game logic on the front end and send the results to the database)


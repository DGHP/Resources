'object' means something completely different in Python and in JavaScript. In JavaScript, an object is a collection of key-value pairs. In Python, they would call this a __dictionary__. In Python, the word object essentially just means 'thing'. The closest that JavaScript has to Python objects is __values__. In Python, you would say that the value 5 is an object.

'class' is also used differently in the two languages. JavaScript has classes, but they're hacky - you can forget about them. The closest thing that JavaScript has to Python classes is _prototypes_. A Python class is like a template for an object: it is from classes that you create objects. When you create an object from a class, you _initialize_ the class. 

You iniialize a class by calling it like a function. If you provide arguments to the class name when you initialize it, these are passed to the class's ```__init__()``` method. 

Classes can also _inherit_ from one another. If class A inherits from class B, an instance of class A will have the methods and properties of an instance of class B, as well as the methods and properties defined specifically for class A. To indicate inheritance, put then name of the parent class in the child class's parameter list when defining the class. 


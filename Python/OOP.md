`__dict__` is a dictionary. Another built-in property worth mentioning is `__name__`, which is a string.
```python
class Classy:
    pass


print(Classy.__name__)
obj = Classy()
print(type(obj).__name__)
```
`__bases__` is a tuple. The tuple contains classes (not class names) which are direct superclasses for the class.
```python
class SuperOne:
    pass


class SuperTwo:
    pass


class Sub(SuperOne, SuperTwo):
    pass


def printBases(cls):
    print('( ', end='')

    for x in cls.__bases__:
        print(x.__name__, end=' ')
    print(')')


printBases(SuperOne)
printBases(SuperTwo)
printBases(Sub)
```
`__module__` is a string, too - it stores the name of the module which contains the definition of the class.
# Reflection and introspection

All these means allow the Python programmer to perform two important activities specific to many objective languages. They are:

- **introspection**, which is the ability of a program to examine the type or properties of an object at runtime;
- **reflection**, which goes a step further, and is the ability of a program to manipulate the values, properties and/or functions of an object at runtime.

In other words, you don't have to know a complete class/object definition to manipulate the object, as the object and/or its class contain the metadata allowing you to recognize its features during program execution.

# Inheritance: issubclass()

Python offers a function which is able to **identify a relationship between two classes**, and although its diagnosis isn't complex, it can **check if a particular class is a subclass of any other class**.

This is how it looks:

`   issubclass(ClassOne, ClassTwo)       `  

The function returns True if `ClassOne` is a subclass of `ClassTwo`, and False otherwise.

```python
   isinstance(objectName, ClassName)       
``` 

The functions returns True if the object is an instance of the class, or False otherwise.

```python
  object_one is object_two      
```  

**The `is` operator checks whether two variables (`object_one` and `object_two` here) refer to the same object**.

>**Note:** the situation in which **the subclass is able to modify its `superclass` behavior (just like in the example) is called `polymorphism`**.


Inheritance is not the only way of constructing adaptable classes. You can achieve the same goals (not always, but very often) by using a technique named composition.

**Composition is the process of composing an object using other different objects**. The objects used in the composition deliver a set of desired traits (properties and/or methods) so we can say that they act like blocks used to build a more complicated structure.

# Single inheritance vs. multiple inheritance

As you already know, there are no obstacles to using multiple inheritance in Python. You can derive any new class from more than one previously defined classes.

There is only one "but". The fact that you can do it does not mean you have to.

Don't forget that:

- a single inheritance class is always simpler, safer, and easier to understand and maintain;
  
- multiple inheritance is always risky, as you have many more opportunities to make a mistake in identifying these parts of the superclasses which will effectively influence the new class;
  
- multiple inheritance may make overriding extremely tricky; moreover, using the `super()` function becomes ambiguous;
  

  
  

  

- multiple inheritance violates the **single responsibility principle** (more details here: [https://en.wikipedia.org/wiki/Single_responsibility_principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)) as it makes a new class of two (or more) classes that know nothing about each other;
  
- we strongly suggest multiple inheritance as the last of all possible solutions - if you really need the many different functionalities offered by different classes, composition may be a better alternative.
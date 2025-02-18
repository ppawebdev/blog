---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Programming Languages", "Python" ]
date: 2019-02-11
description: "A tutorial on Python classes and object-orientated design in Python."
draft: false
lastmod: 2019-03-25
tags: [ "Python", "programming", "programming languages", "software", "OOP", "object orientated", "class", "design", "issubclass" ]
title: "Python Classes And Object Orientated Design"
type: "page"
---

<p>Since Python v3.3, you can use both the `@staticmethod` and `@abstractmethod` decorators on the same class function (and the `@abstractstaticmethod` decorator has been depreciated).</p>

{{< highlight python >}}
import abc

class MyClass:

    @staticmethod
    @abstractmethod
    def my_func():
        pass
{{< /highlight >}}

{{% note %}}
You have to make sure to specify `@staticmethod` before `@abstractmethod` or it will not work.
{{% /note %}}

<h2>Checking If A Class Is A Subclass Of Another</h2>

<p>You can check if one class is a sub-class of another with the <code>issublass()</code> function:</p>

{{< highlight python >}}
class ParentClass:
    pass

class ChildClass(ParentClass):
    pass

class StandaloneClass:
    pass

print(issubclass(ChildClass, ParentClass))
# stdout: True

print(issubclass(StandaloneClass, ParentClass))
# stdout: False

# Works with variables which are assigned to a class too
my_class = ChildClass
print(issubclass(my_class, ParentClass))
# stdout: True
{{< /highlight >}}

<h2>Class Variables</h2>

<p>In Python, classes can be assigned variables, either statically or dynamically. The important difference between assigning variable to A class and assigning variables to an INSTANCE of a class is that <b>class variables are shared between all variables/instances of that class, while instance variables are unique to that particular instance of the class</b>.</p>

{{< highlight python >}}
class TestClass:
    pass

# Create two class variables (not here that we are NOT)
# creating instances, there are no brackets () at the end)
test_class_1 = TestClass
test_class_2 = TestClass

# Assign a value to a class variable
test_class_1.my_var = 2

# The other class variable now has this value too!
print(test_class_2.my_var)
# stdout: 2

test_class_2.my_var = 3
# The original classes variable has changed, as the variable is shared
# between all identical class objects
print(test_class_1.my_var)
# stdout: 3
{{< /highlight >}}

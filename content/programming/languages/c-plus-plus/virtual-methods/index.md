---
authors: [ "Geoffrey Hunter" ]
date: 2013-12-25
draft: false
title: Virtual Methods
type: page
---

## What Are Virtual Methods?

Virtual methods allow inherited methods of classes to be overwritten, even when a pointer to the base class is used. You can overwrite methods without using the virtual descriptor, just by using the same name, but the overwritten methods will not be called when a pointer to the base class is used. Real virtual methods are virtual methods that require implementation by a derived class.

## Pure Virtual Methods

_Pure virtual methods_ are virtual methods which do not have any body (definition) defined for them in a particular class. They can be defined by adding an = 0 to the end of the declaration of the virtual method in the class header file, as shown below:

```c++    
class AbstractClass {
protected:
    // This is a PURE VIRTUAL method
    virtual void MyMethod() = 0;
};
```

Any class which has one or more pure virtual methods is called an **abstract class**. You cannot create objects of an abstract class. To use an abstract class, you must create another class which inherits from the pure virtual methods and defines a body for them, as shown in the code below:

```c++    
class ConcreteClass : AbstractClass {
public:
    void MyMethod() override {
        std::cout << "Hello" << std::endl;
    }
};
```

## The override Keyword

C++11 introduced the override keyword, which is very useful when designing applications that use virtual methods. The override keyword makes the compiler check that the stated method overrides a base class. If it doesn't, you get a compiler error.

```c++    
class AbstractClass {
protected:
    virtual void MyMethod() = 0;
};

class ConcreteClass : AbstractClass {
public:
    void MyMethod() override { // This WILL compile fine
        std::cout << "Hello" << std::endl;
    }

    void BogusMethod() override { // This WON'T compile
        std::cout << "Hello" << std::endl;
    }
};
```

The override keyword prevents mistakes where you expected a method to be overridden but was not because of a typo or type mismatch, which can cause subtle but incorrect runtime behaviour.

Note: If you use the override keyword, you do not also need to specify the method as virtual (as this is implied).

For more information about the override keyword, see [http://en.cppreference.com/w/cpp/language/override](http://en.cppreference.com/w/cpp/language/override).

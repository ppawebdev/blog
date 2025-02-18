---
authors: [ "Geoffrey Hunter" ]
date: 2013-11-18
draft: false
title: Type Conversion
type: page
---

## C-Style Casting

C++ supports basic C-style casting. C-style casting is in the form:

```c++   
int num1 = 5;
double num2 = (double)5;
```

It also adds a new way of performing this type of casting, called by some "function-style casting", where the brackets go around the variable rather than the type:

```c++    
int num1 = 5;
double num2 = double(num1); // Notice brackets enclose the variable, not the type
```

## C++ Casting Operators

C++ introduces four new ways of casting (compared to C). This includes `static_cast`, `dynamic_cast`, `reinterpret_cast` and `const_cast`.

**static_cast**

`static_cast` can perform conversions between related pointers. It can _upcast_, which is a cast from a pointer-to-derived class to a pointer-to-base, and also _downcast_, which is a cast from a pointer-to-base class to a pointer-to-derived class.

No runtime checks are performed to make sure the type being casted to is a complete instance (as opposed to `dynamic_cast`). It is up to the user to make sure the cast is appropriate. The common example of this mistake is when you perform a down conversion to a derived type when the object is only of the base type:

```c++    
class Base {};
class Derived: public Base {};
Base * a = new Base;
Derived * b = static_cast<Derived*>(a);
```

`static_cast` can convert between any pointer and the type void*. It is guaranteed that if you convert a pointer to an object to `void*` and then back again, the pointer will still be valid. This technique works great for passing data when the data type may vary (e.g. passing data on message queues between threads). See [https://github.com/gbmhunter/CppUtils/blob/master/include/CppUtils/MsgQueue.hpp](https://github.com/gbmhunter/CppUtils/blob/master/include/CppUtils/MsgQueue.hpp) for an example of this.


`static_cast` is also useful for converting between C++'s strongly typed enums (`enum class { ...`) and integers.

```c++    
enum class Colors {
    RED,
    GREEN
};

int main() {
    int fail = (int)Colors::GREEN; // This will produce a compiler error
    int pass = std::static_cast<int>(Colors::GREEN); // This works, int = 1

    // We can also convert the other way
    Colors color = std::static_cast<Colors>(0); // color = Colors::RED
}
```

**dynamic_cast**

`dynamic_cast` can _upcast_ and _downcast_ just like `static_cast`, except that it uses runtime type information (RTTI) to make sure the classes are compatible before performing a downcast. If the class cannot be downcasted (because it is an instance of the base class only, and not the derived class), then dynamic_cast returns `nullptr`.

For this reason, `dynamic_cast` is predominately used to _try_ to convert a base object into a derived object.

`dynamic_cast` requires RTTI to be enabled to keep track of what type each object is. Some environments disable RTTI (e.g. low-resource embedded environments) and therefore dynamic_cast may not be available for use in some software.

If `dynamic_cast` cannot cast a pointer, it returns `nullptr`. If it cannot cast a reference, it throws the exception `std::bad_cast`.
 
> [C++11: 5.2.7/9]: The value of a failed cast to pointer type is the null pointer value of the required result type. A failed cast to reference type throws std::bad_cast (18.7.2).

**reinterpret_cast**

`reinterpret_cast` can convert a pointer to any type to a pointer of any other type. All it does is essentially remaps the underlying data structure to the type. Obviously, this is a dangerous operation and should be only used with extreme care. It can have implementation specific consequences.

It can also be used to cast pointers to integer types. This can be useful if you want to convert the value of the pointer to a string. The size and representation of the integer is platform specific, but is guaranteed to be held within a `std::intptr_t` type. It is also guaranteed to be valid if cast back to a pointer again.

**const_cast**

`const_cast` removes the `const` modifier from a variable. It is undefined behaviour to then modify an object

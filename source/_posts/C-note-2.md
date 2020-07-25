---
title: C++ note 2
date: 2020-09-10 16:59:59
tags: [cpp]
---
### 'this' Pointer:

1. Passed as a hidden argument to all non-static member function calls and is available as a local variable within the body of all non-static functions.
2. `this` is a const pointer.
3. Objects can destroy themselves by calling the following code `delete this;`. 

### Concept:
1. **C++ polymorphism** means that a call to a member function will cause a different function to be executed depending on the type of object that invokes the function.

### Function overloading:
1. In C++, following function declarations [cannot be overloaded](https://www.geeksforgeeks.org/function-overloading-in-c/).
    - Function declarations that differ only in the return type.
    - Member function declarations with the same name and the name parameter-type-list cannot be overloaded if any of them is a static member function declaration.
    - Parameter declarations that differ only in a pointer * versus an array [] are equivalent.
    - Parameter declarations that differ only in that one is a function type and the other is a pointer to the same function type are equivalent.
    - Parameter declarations that differ only in the presence or absence of const and/or volatile are equivalent.
    - Two parameter declarations that differ only in their default arguments are equivalent. 
2. C++ allows member methods to be overloaded on the basis of const type. Overloading on the basis of const type can be useful when a function return reference or pointer.

### Static:
1. Static methods can only access static members (data and methods)


### Inheritence:
1. Assume that an integer takes 4 bytes: `sizeof(derived)` is 80. Since b1 and b2 both inherit from class base, two copies of class base are there in class derived.
    ```
    class base {
        int arr[10];
    };
    class b1: public base { };
    class b2: public base { };
    class derived: public b1, public b2 {};
    ```
2. Assume that an integer takes 4 bytes: `sizeof(derived)` is 48. 8 extra bytes are for bookkeeping information stored by the compiler.
    ```
    class base {
      int arr[10];     
    };
    class b1: virtual public base { };
    class b2: virtual public base { };
    class derived: public b1, public b2 {};
     ```
3. If there is multilevel inheritance, then function is linearly searched up in the inheritance hierarchy until a matching function is found.
4. A base class pointer can point to a derived class object, but we can only access base class member or virtual functions using the base class pointer.
5. If a derived class writes its own method, then all functions of base class with same name become hidden, even if signaures of base class functions are different. We can access base class functions using scope resolution operator even if they are made hidden by a derived class function. `Derived d; d.Base::fun(5);`
6. When we assign an object of derived class to an object of base type, the derived class object is **sliced** off and all the data members inherited from base class are copied.
7. The base class members cannot be directly assigned using initializer list. We should call the base class constructor in order to initialize base class members.
8. This is a typical example of diamond problem of multiple inheritance. Here the base class member 'a' is inherited through both Derived1 and Derived2. So there are two copies of 'a' in DerivedDerived which makes the statement "cout << a;" ambiguous.
    ```
    class Base
    {
    protected:
        int a;
    public:
        Base() {a = 0;}
    };
    class Derived1:  public Base
    {
    public:
        int c;
    };
    class Derived2:  public Base
    {
    public:
        int c;
    };
    class DerivedDerived: public Derived1, public Derived2
    {
    public:
        void show()  {   cout << a;  }
    };
    int main(void)
    {
        DerivedDerived d;
        d.show();
        return 0;
    }
    ```
    
### Virtual:
1. If a class has a pure virtual function, it becomes an abstract class and an instance of it cannot be created.
2. If we don't override the pure virtual function in derived class, then derived class also becomes abstract class.
3. There is nothing like Virtual Constructor. Making constructors virtual doesn't make sense as constructor is responsible for creating an object and it can’t be delegated to any other object by virtual keyword means.
4. A destructor can be virtual. We may want to call appropriate destructor when a base class pointer points to a derived class object and we delete the object. If destructor is not virtual, then only the base class destructor may be called. If the destructor is vitrual, the derived class destructor is called which in turn calls base class destructor.
    ```
    Base *Var = new Derived();
    delete Var;
    // but below will call both
    {
        Derived Var;
    }
    ```
5.  Compiler places a VPTR with every object.
6.  When a class has a virtual function, functions with same signature in all descendant classes automatically become virtual. 

### Const:
1. A const object can only call const functions.
2. `const char* a = "Anthony";`
    is:
    ```
    const char string_literal[] = "Anthony";
    const char *a = string_literal;
    ```

### New & Delete:
1. It is undefined behavior to call delete twice on a pointer. Anything can happen, the program may crash or produce nothing.

### Exception handling:
1. try, catch, and throw:
    **throw** − A program throws an exception when a problem shows up. This is done using a throw keyword.
    **catch** − A program catches an exception with an exception handler at the place in a program where you want to handle the problem. The catch keyword indicates the catching of an exception.
    **try** − A try block identifies a block of code for which particular exceptions will be activated. It's followed by one or more catch blocks.
2. If both base and derived classes are caught as exceptions then catch block of derived class must appear before the base class. If we put base class first then the derived class catch block will never be reached. 
3. Note that the implicit type conversion doesn't happen when exceptions are caught. eg. The character is not automatically converted to int.
4. It is compiler error to put catch all block before any other catch. The catch(...) must be the last catch block.
5. The statement `throw;` is used to re-throw an exception:
    ```
    try {
        try
        {
            throw 20;
        }
        catch (int n)
        {
            cout << "Inner Catchn";
            throw;
        }
    }
    catch (int x)
    {
        cout << "Outer Catchn";
    }
    ```
6. When an object is created inside a try block, destructor for the object is called before control is transferred to catch block.
7. When an exception is thrown and not caught, the program terminates abnormally.

### Friend:
1. Friendship is not inherited.


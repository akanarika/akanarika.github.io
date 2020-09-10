---
title: C++ note 1
date: 2020-09-10 00:38:08
tags: [cpp]
---
### Constructor:
1. In C++, if we do not write our own, then compiler automatically creates a default constructor, a copy constructor and an assignment operator for every class. If we write any constructor, then compiler doesn't create the default constructor.
2. When is copy constructor called?
    - When an object of the class is returned by value.
    - When an object of the class is passed (to a function) by value as an argument.
    - When an object is constructed based on another object of the same class.
    - When compiler generates a temporary object.
    - (Note: It is however, not guaranteed that a copy constructor will be called in all these cases, because the C++ Standard allows the compiler to optimize the copy away in certain cases, one example being the return value optimization (sometimes referred to as RVO). [RVO](https://en.wikipedia.org/wiki/Copy_elision#Return_value_optimization) is a compiler optimization that involves eliminating the temporary object created to hold a function's return value.)
3. When should we write our own assignment operator in C++?
    - The answer is same as Copy Constructor. If a class doesn’t contain pointers, then there is no need to write assignment operator and copy constructor. 
    - (Note: [Self assignment](https://isocpp.org/wiki/faq/assignment-operators))
4. Assignment operator & Copy constructor
    ```cpp
    class Point {
    public:
        Point() { cout << "Normal Constructor calledn"; }
        Point(const Point &t) { cout << "Copy constructor calledn"; }
    };
 
    Point *t1, *t2;   // No constructor call
    t1 = new Point(10, 15);  // Normal constructor call
    t2 = new Point(*t1);   // Copy constructor call 
    Point t3 = *t1;  // Copy Constructor call
                    // ('X b = a;' calls copy constructor
                    // and is same as 'X b(a);')
    Point t4;   // Normal Constructor call
    t4 = t3;   // Assignment operator call 
    ```
5. Copy constructor: Objects must be passed by reference in copy constructors. Compiler checks for this and produces compiler error if not passed by reference. Also, copy constructor argument should be const.
    ```cpp
    #include<iostream>
    using namespace std;
    class Point {
        int x;
    public:
        Point(int x) { this->x = x; }
        Point(const Point p) { x = p.x;} // Compiler Error: p must be passed by reference
        int getX() { return x; }
    };
    ```
6. When do we use [Initializer List](https://www.geeksforgeeks.org/when-do-we-use-initializer-list-in-c/) in C++?
    - For initialization of non-static const data members.
    - Reference members must be initialized using Initializer List.
    - For initialization of member objects which do not have default constructor.
    - For initialization of base class members.
    - When constructor’s parameter name is same as data member, either use this pointer or Initializer List
    - Performance reasons: It is better to initialize all class variables in Initializer List instead of assigning values inside body.
7. Constructors cannot be virtual.
8. If a class has a constructor which can be called with a single argument, then this constructor becomes conversion constructor because such a constructor allows automatic conversion to the class being constructed. 
9. Consider the following statement `Test *ptr = new Test; ` There are actually two things that happen in the above statement--memory allocation and object construction; the new keyword is responsible for both. One step in the process is to call operator new in order to allocate memory; the other step is to actually invoke the constructor. Operator new only allows us to change the memory allocation method, but does not do anything with the constructor calling method. Keyword new is responsible for calling the constructor, not operator new.

### Destructor:
1. Destructors can be private. then `Test t;` would compile error, `Test *t;` would be fine.
2. There can be only one destructor in a class.

### Reference:
1. When a function returns by reference, it can be used as lvalue. Since x is a static variable, it is shared among function calls and the initialization line "static int x = 10;" is executed only once. The function call fun() = 30, modifies x to 30. The next call "cout << fun()" returns the modified value.
    ```cpp
    #include<iostream>
    using namespace std;
     
    int &fun()
    {
        static int x = 10;
        return x;
    }
    int main()
    {
        fun() = 30;
        cout << fun();
        return 0;
    }
    ```
    
2. Since we return reference to a local variable, the memory location becomes invalid after function call is over. Hence it may result in segmentation fault runtime error.
    ```cpp
    #include<iostream>
    using namespace std;
     
    int &fun()
    {
        int x = 10;
        return x;
    }
    int main()
    {
        fun() = 30;
        cout << fun();
        return 0;
    }
    ```
    
### Class:
1. The size of an empty class not zero, it is 1 byte generally. It is nonzero to ensure that the two different objects will have different addresses.
2. The static variables are stored in the data segment of the memory. The data segment is a part of the virtual address space of a program. All the static variables that do not have an explicit initialization or are initialized to zero are stored in the uninitialized data segment( also known as the BSS segment).
3. Which of the following is not correct for virtual function in C++ ?
(A) Must be declared in public section of class.
(B) Virtual function **can't** be static.
(C) Virtual function should be accessed using pointers.
(D) Virtual function is defined in base class.
4. Association, Composition, Aggregation
    - **Association**
Association refers to the relationship between multiple objects. It refers to how objects are related to each other and how they are using each other's functionality. Composition and aggregation are two types of association.
    - **Composition**
The composition is the strong type of association. An association is said to composition if an Object owns another object and another object cannot exist without the owner object. Consider the case of Human having a heart. Here Human object contains the heart and heart cannot exist without Human.
    - **Aggregation**
Aggregation is a weak association. An association is said to be aggregation if both Objects can exist independently. For example, a Team object and a Player object. The team contains multiple players but a player can exist without a team.
5. Interfaces (Abstract Classes)
    - A class is made abstract by declaring at least one of its functions as pure virtual function.
    - Abstract classes cannot be used to instantiate objects and serves only as an interface. Attempting to instantiate an object of an abstract class causes a compilation error.
    - If a subclass of an ABC needs to be instantiated, it has to implement each of the virtual functions, which means that it supports the interface declared by the ABC. Failure to override a pure virtual function in a derived class, then attempting to instantiate objects of that class, is a compilation error.

### Template:
1. When the compiler encounters this call to a template function, it uses the template to automatically generate a function replacing each appearance of myType by the type passed as the actual template parameter (int in this case) and then calls it. This process is automatically performed by the compiler and is invisible to the programmer.
2. The format for declaring function templates with type parameters is (indistinct):
    ```
    template <class identifier> function_declaration;
    template <typename identifier> function_declaration;
    ```
3. Template for Class
    ```
    template <class T>
    class mypair {
        T values [2];
      public:
        mypair (T first, T second)
        {
          values[0]=first; values[1]=second;
        }
    };
    ```
4. Non-type parameters for templates
    ```
    template <class T, int N>
    class mysequence {
        ...
    };
    mysequence <double, 5> myints;
    ```
5. Because templates are compiled when required, this forces a restriction for multi-file projects: the implementation (definition) of a template class or function must be in the same file as its declaration.

### Operator overloading:
1. cout is an object of ostream class which is a compiler defined class. When we do "cout << obj" where obj is an object of our class, the compiler first looks for an operator function in ostream, then it looks for a global function. One way to overload insertion operator is to modify ostream class which may not be a good idea. So we make a global method.
    ```
    ostream & operator << (ostream &out, const Complex &c)
    {
        out << c.real;
        out << "+i" << c.imag;
        return out;
    }
    ```


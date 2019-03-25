---
title: const T& xx
date: 2017-05-29 01:24:55
tags: [cpp]
---
Start on a new page. Following [Scratchapixel](https://www.scratchapixel.com) to review and learn graphics. In the first lesson, a constructor

```c++
Vec3(const T &xx) : x(xx), y(xx), z(xx) {} 
```
in class Vec3 is used. As a weak learner of c++, I'm confused about the parameter passing here. Why using const T &xx?
An answer on the stack overflow solved my question.

[post](https://stackoverflow.com/questions/2627166/difference-between-const-reference-and-normal-parameter)
What's the difference?

```c++
void DoWork(int n);
void DoWork(const int &n);
```

Answer:
The difference is more prominent when you are passing a big struct/class.

```c++
struct MyData {
    int a,b,c,d,e,f,g,h;
    long array[1234];
};
void DoWork(MyData md);
void DoWork(const MyData& md);
```
When you use use 'normal' parameter, you pass the parameter by value and hence creating a copy of the parameter you pass. if you are using const reference, you pass it by reference and the original data is not copied.
In both cases, the original data cannot be modified from inside the function.
EDIT:
In certain cases, the original data might be able to get modified as pointed out by Charles Bailey in his answer.

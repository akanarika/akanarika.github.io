---
title: 'C++ note 4 - Shared Pointer '
date: 2020-09-10 22:08:54
tags: [cpp]
---
### Shared pointer:
```
#include <iostream>

class RC
{
private:
    int count;
public:
    RC() : count(0) {}
    
    int add() {
        return ++count;
    }
    
    int remove() {
        return --count;
    }
    
    int get() {
        return count;
    }
};

template <class T>
class SP
{
private:
    T* data;
    RC* rc;
    
public:
    explicit SP(T* d) : data(d), rc(new RC()) {
        rc->add();
    }
        
    
    SP(const SP<T>& sp) : data(sp.data), rc(sp.rc) {
        rc->add();
    }
    
    ~SP() {
        if (rc->remove() == 0) {
            delete data;
            delete rc;
        }
    }
    
    SP<T>& operator = (const SP<T>& sp) {
        if (this == &sp) return *this;
        
        if (rc->remove() == 0) {
            delete data;
            delete rc;
        }
        
        data = sp.data;
        rc = sp.rc;
        rc->add();
        return *this;
    }
    
    void print() {
        std::cout << "data: " << *data << std::endl;
        std::cout << "count: " << rc->get() << std::endl;
    }
  
};

int main()
{
    SP<int> sp(new int(5));
    sp.print();
  
    SP<int> sp2 = sp;
    sp2.print();
    
    SP<int> sp3(new int(4));
    sp3 = sp;
    sp3.print();
  
    return 0;
}
```

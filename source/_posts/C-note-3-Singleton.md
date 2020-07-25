---
title: C++ note 3 - Singleton
date: 2020-09-10 17:42:27
tags: [cpp]
---
### Singleton:
1. Singleton design pattern is a software design principle that is used to restrict the instantiation of a class to one object. This is useful when exactly one object is needed to coordinate actions across the system
2. Can act just like namespace
3. A simple implementation:
    ```
    class Singleton
    {
        private:
            Singleton() {} // Disable from instantiating

            static Singleton Instance;
            
        public:
            static Singleton& Get() {
                return s_Instance;
            }
            void Func();
    };
    
    Singleton Singleton::s_Instance;
    
    int main()
    {
        Singleton::Get().Func();
        return 0;
    }
    ```
4. Issues from above:
    - One can do `Singleton instance = Singleton::Get();` instead of `Singleton& instance = Singleton::Get();` will copy all data in the Singleton and create an additional Singleton. Should mark the copy constructer, and the assignment operator as delete.
    ```
    class Singleton
    {
        private:
            Singleton() {} // Disable from instantiating

            static Singleton Instance;
            
        public:
            Singleton(const Singleton&) = delete; // solve the issue
            Singleton& operator=(const Singleton&) = delete;
            static Singleton& Get() {
                return s_Instance;
            }
            void Func();
    };
    ```
5. Can remove the global initialization and create inside `Get()`.
    ```
    class Singleton
    {
        private:
            Singleton() {} // Disable from instantiating
        public:
            Singleton(const Singleton&) = delete;
            Singleton& operator=(const Singleton&) = delete;
            static Singleton& Get() {
                static Singleton s_Instance; // Init from here
                return s_Instance;
            }
            void Func();
    };
    ```

6. A final version:
    ```
    #include <iostream>
    
    class Singleton
    {
        private:
            Singleton() {} // Disable from instantiating
        public:
            Singleton(const Singleton&) = delete;
            Singleton& operator=(const Singleton&) = delete;
            static Singleton& Get() {
                static Singleton s_Instance; // Init from here
                return s_Instance;
            }
            void Func() {
              std::cout << "Func called" << std::endl;
            };
    };
    
    int main()
    {
      Singleton::Get().Func();
      return 0;
    }
    ```

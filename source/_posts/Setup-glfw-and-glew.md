---
title: Setup glfw and glew
date: 2017-02-15 23:02:17
tags: [notes]
---
I used OpenGL more than once before. However, every time I have to start a new OpenGL project, it would be like the first time. Because I will encounter so many new problems or old which I don't remember. Today I used XCode to build a very simple program, but there turned out to be some fresh errors. 
```
Undefined symbols for architecture x86_64:
  "_glewExperimental", referenced from:
      _main in main-8eb2b0.o
  "_glewInit", referenced from:
      _main in main-8eb2b0.o
  "_glfwCreateWindow", referenced from:
      _main in main-8eb2b0.o
  "_glfwInit", referenced from:
      _main in main-8eb2b0.o
  "_glfwMakeContextCurrent", referenced from:
      _main in main-8eb2b0.o
  "_glfwTerminate", referenced from:
      _main in main-8eb2b0.o
  "_glfwWindowHint", referenced from:
      _main in main-8eb2b0.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```
Actually they are not special at all. It's just because those libraries were not completely installed or linked(I guess). But the challenge today is my Homebrew and Macport also broke down like they intend(probrably because I haven't used them for a long time). Then to solve the problem. I used the very universal solution: reinstall everything - homebrew, macport, glew, glfw3. Then it worked. But it took me incredibly hours.
```bash
gcc -o main main.cpp -framework OpenGL -framework GLUT -lGLEW -lglfw3
```

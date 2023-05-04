###Cmake介绍

CMake 是一种跨平台编译工具，比 make 更为高级，使用起来要方便得多。CMake 主要 是编写 CMakeLists.txt 文件，然后用 cmake 命令将 CMakeLists.txt 文件转化为 make 所需要的 makefile 文件，最后用 make 命令编译源码生成可执行程序或共享库（so(shared object)）。 因此 CMake 的编译基本就两个步骤：

```cmake
cmake
make
```

创建CMakeLists.txt文件

```
project(helloworld) # 指定项目名称
add_executable(helloworld ./main.cpp) # 指定生成可执行文件
```

CMake语法中大小写不敏感

```
PROJECT(helloworld)
ADD_EXECUTABLE(helloworld ./main.cpp)
```

创建一个build并且进入到build文件夹中执行

```
cmake ..
make
```

经过上述操作，文件已经被编译成可执行文件，直接执行即可



对于设置的项目名称也可以写成如下格式：

![image-20230504205026883](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230504205026883.png)
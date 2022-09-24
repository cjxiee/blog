# Slam study

## Lec 1
### Some operation in linux
#### Basic

1. Create an empty cpp file

    touch main.cpp
      
2. Edit this file

      vim main.cpp    /   gedit main.cpp
3. Complie

      g++ main.cpp
4. Run the file

      ./a.out

#### CMake

    cmake .      # generate a makefile which is used to compile the proejct
    make         # compile the project
    
    or
    
    cmake -B build
    cmake --build build
   
   
   ##### CMakeLists.txt
   
    cmake_minimum_required(VERSION 3.10)

    project(CMake_tutorial)

    add_executable(helloslam main.cpp)    # define executable file

    add_executable(useHello useHello.cpp)

    add_library(hello hello.cpp)        # add the user-defined lib  (** create .cpp file and .h file) 库文件和头文件（提供函数的声明）

    target_link_libraries(useHello hello)   # link the lib to executable file


    只要有头文件和库文件来生成一个库，再将这些文件连接到可执行文件
    
    
    
#### Using Vscode 
Remember to include the linked lib or cpp direction in the "tasks.json" file
        
        "${workspaceFolder}/*.cpp"
        "${fileDirname}/*.cpp"
   

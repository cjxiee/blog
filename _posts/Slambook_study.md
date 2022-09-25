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
   
   
   
## Lec2
### Install Sophus lib
Check this url https://blog.csdn.net/weixin_44684139/article/details/104803225?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-104803225-blog-116547361.pc_relevant_multi_platform_whitelistv4&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-104803225-blog-116547361.pc_relevant_multi_platform_whitelistv4&utm_relevant_index=5 for reference.

Install fmt and then Sophus
    

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

### visualizeGeometry and plotTrajectory compile error

    原因：其中引用的sigslot/signal.hpp是基于C++14标准的，而原CMakeLists.txt中的设置的标准为C++11。
    
    
### fix <Eigen/Core> error

    sudo ln -s /usr/include/eigen3/Eigen /usr/include/Eigen
    
    
## Lec3
###  Issue: fmt is not linked

    fmt package has been used in Sophus, so in fmt should be linked to the executable file in the CMakefile.txt
    
    find_package(fmt REQUIRED)
    target_link_libraries(xxxxxx fmt::fmt)
    
###  CMakeFiles.txt some notes
Check this link https://stackoverflow.com/questions/43456982/cmake-what-is-the-difference-between-include-directories-versus-target-link
Unless a library is a header-only library, call to target_link_libraries is required for use it.

     if we include the directies, it will be unnecessary to link the lib:
     
     include_directories(${Sophus_INCLUDE_DIRS})
     
     instead of
     
     target_link_libraries(${Sophus_INCLUDE_LIBRARIES}(Sphous::Sphous))
     
## Lec4
###  Some notes about c++:
    
    #### understand the structure of image in c++
    int **x = new int*[3];     // x store the address of the head pointer of each row
    for(int i =0; i<3; i++){
        x[i] = new int[4];
    }
    
### Point Cloud
    
    When the intrinsic and extrinsic parameters are provided, it is easy to reconstruct the 3D point cloud.
    
    Known: color image, depth image and carmera pose of each image being taken.
    
    Convert the location of pixel in the image plane to the location in the 3D world, using the knowledge of intrinsic parameters(fx, fy, cu, cv) and depth of each pixel. Store the each point within a 6D vector including position and color infomation. Iterate over all pixel and then point cloud can be easily plotted. Here is a sample image from slambook2/ch5.

file:///home/cjxie/Desktop/Screenshot%20from%202022-09-28%2006-43-07.png

    
#### Exist Issue: noise of depth measurement 

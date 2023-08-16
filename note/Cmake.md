# **Cmake** 

该项目的 `CMakeLists.txt` 中需要添加以下内容：

```
cmake_minimum_required(VERSION 3.5)  //CMake需要的最小版本，可在命令行中输入cmake --version获取
project (<project_name>)  //指定工程名称
add_executable(<executable_name> <cppfile_name>) //生成可执行文件
```

使用CMakeLists.txt 生成makefile

```
cmake CMakeLists.txt //目录下会生成一个Makefile文件
make  //将源代码编译生成可执行文件（文件名为上述<executable_name>）
./<executable_name>  //运行该执行文件
```

`make help` 查看使用当前的Makefile所能执行的所有指令



语法总结：

- `set(<variable> <value>)` 设置变量
- `target_include_directories(<project_name> <INTERFACE|PUBLIC|PRIVATE> <headfile_directory>)` 指定所要包含的头文件
- `message("your message")` 在终端打印信息
- `add_library(<library_name> STATIC <cppfile_name>)` 生成静态库
- `target_link_libraries(<executable> <INTERFACE|PUBLIC|PRIVATE> <library_name>)` 指定所要链接的库
- `add_library(<library_name> SHARED <cppfile_name>)` 生成动态库
- `find_package(<package_name>)` 查询第三方库的位置

```
mkdir build
cd build
cmake ..  # 使用的是上一层目录的CMakeLists.txt，因此需要输入'..'
make
```

将生成的静态库、可执行文件输出到build 文件夹里，而不是和主项目混杂在一起。



CMake支持的所有第三方库可以在 https://cmake.org/cmake/help/latest/manual/cmake-modules.7.html 中找到
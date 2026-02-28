# cmake

c/c++ 跨平台的安装（编译）工具，输出各种各样的makefile或者project文件  

安装：  
`sudo apt install cmake`

官网：[Cmake](https://cmake.org/)

---
# 使用
## 终端构建
适用于工程项目编译

通常把编译文件放在`build`目录下
```bash
mkdir build
cd build
cmake ..
cmake -G Ninja ..
```
## GUI构建
适用于库源文件编译

- 打开cmake-gui
- 选择源文件目录
- 选择构建目录
- configure选择编译器
- 设置构建选项
- generate启动构建生成makefile

## 编译和安装
```bash
cd build
make -j$(nproc)

make install
```
---

# Toolchain.cmake
配置编译器工具链，实现交叉编译
创建示例 `toolchain.cmake`：
```
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR arm)

set(TOOLCHAIN_DIR       	/usr)
#set(CMAKE_SYSROOT       	${TOOLCHAIN_DIR}/arm-linux-gnueabihf)

# 指定交叉编译器 arm-linux-gcc 和 arm-linux-g++
set(CMAKE_C_COMPILER        ${TOOLCHAIN_DIR}/bin/arm-linux-gnueabihf-gcc)
set(CMAKE_CXX_COMPILER		${TOOLCHAIN_DIR}/bin/arm-linux-gnueabihf-g++)

set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)

```

运行示例：
```bash
cmake -DCMAKE_TOOLCHAIN_FILE=../toolchain.cmake ..
```

---

# `CMakeLists.txt`
这是一个构建脚本文件，用于 `CMake` 这个跨平台的自动化建构系统。`CMake` 用于控制编译过程，通过使用通用的构建规则，使得软件编译、测试和打包的过程可以在多种平台上重复执行。

## 内容示例
```
cmake_minimum_required(VERSION 3.0)

project(MqttClient VERSION 1.0.1)

# 使用C++11标准
set(CMAKE_CXX_STANDARD 11)
# 时间戳
string(TIMESTAMP COMPILE_TIME %Y%m%d-%H%M%S)
# 宏定义 USE_THE_CMAKE
add_definitions(-D USE_THE_CMAKE)

# 添加 mosquittopp 库
find_library(MOSQUITTO_LIB mosquittopp)
if(MOSQUITTO_LIB)
	message(STATUS "mosquittopp library found: ${MOSQUITTO_LIB}")
else()
	message(FATAL_ERROR "mosquittopp library not found!")
endif()

# 添加所有当前目录的源文件
aux_source_directory(. DIR_SRCS)

# 添加输出执行文件
add_executable(${PROJECT_NAME} ${DIR_SRCS})

# add mosquittopp link
target_link_libraries(${PROJECT_NAME} ${MOSQUITTO_LIB})

# 版本配置文件
configure_file(VersionConfig.h.in VersionConfig.h)
# 包含build/目录下的头文件
target_include_directories(${PROJECT_NAME} PUBLIC
							${PROJECT_BINARY_DIR}
							)


```
## 命令详解

**命令不区分大小写**

### 指定cmake最低版本

1. 指令  

	`cmake_minimum_required`
2. 实例

	`cmake_minimum_required(VERSION 3.15)`
	
### 指定项目名称

1. 指令  

	`project`
2. 实例

	`project(Tutorial VERSION 1.0.1)`
	

### 生成可执行文件

1. 指令  

	`add_executable`
2. 实例

	`add_executable(Tutorial tutorial.cpp)`

### 设置变量

1. 指令  

	`set`
2. 实例

```
# 使用C++11标准
set(CMAKE_CXX_STANDARD 11)
# 设置源文件
set(SRC_LIST a.cpp b.cpp c.cpp)
add_executable(${PROJECT_NAME} ${SRC_LIST})
```

### 添加配置文件

1. 指令  

	`configure_file`
2. 实例
```
# 加入一个配置头文件，用于处理 CMake 对源码的设置
configure_file (
	"${PROJECT_SOURCE_DIR}/config.h.in"
	"${PROJECT_BINARY_DIR}/config.h"
)
```
`PROJECT_BINARY_DIR` 就是 build 所在路径  

### 生成链接库

1. 指令  

	`add_library`
2. 实例
```
# 生成链接库
add_library (MathFunctions ${DIR_LIB_SRCS})
```

### 添加链接库

1. 指令  

	`target_link_libraries`
2. 实例
```
# 添加链接库
target_link_libraries(${PROJECT_NAME} MathFunctions)
```

### 可选项

1. 指令  

	`option(<variable> "description [initial value])`
2. 实例

	`option(USE_TEST "Use option test" ON)`

### 查找源文件

1. 指令  

	`aux_source_directory(<dir> <variable>)`
2. 实例
```
# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)
```

### 查找库文件

1. 指令  

	`find_library`
2. 实例

	```
	find_library(var lib_name lib_path1 lib_path2)
	
	```
	- 函数作用：查找库，并把库的绝对路径和名称存储到第一个参数里
	- 参数var：用于存储查找到的库
	- 参数lib_name：想要查找的库的名称，默认是查找动态库，想要指定查找动态库或静态库,可以加后缀，例如 funcname.so 或 funcname.a 
	- 参数lib_path：想要从哪个路径下查找库，可以指定多个路径，默认 /usr/lib/


### 添加头文件目录

1. 指令  

	`include_directories ( dir )`
2. 实例

```
# 添加 math 子目录
include_directories (math)
```

### 添加子目录

1. 指令  

	`add_subdirectory`
2. 实例

```
# 添加 math 子目录
add_subdirectory(math)
```

### 定制安装规则

1. 指令  

	`install`
2. 实例
```
# 指定安装路径
install (TARGETS Demo DESTINATION bin)
install (FILES "${PROJECT_BINARY_DIR}/config.h"
		DESTINATION include)

```

3. 安装  
	`make install`
	
	生成的 Demo 文件将会被复制到 `/usr/local/bin` 中
	生成的 config.h 文件则会被复制到 `/usr/local/include` 中
	

---

## 为工程添加测试

CMake 提供了一个称为 CTest 的测试工具

1. 示例：
```
# 启用测试
enable_testing()

# 测试程序是否成功运行
add_test (test_run Demo 5 2)

# 测试帮助信息是否可以正常提示
add_test (test_usage Demo)
set_tests_properties (test_usage
  PROPERTIES PASS_REGULAR_EXPRESSION "Usage: .* base exponent")

# 测试 5 的平方
add_test (test_5_2 Demo 5 2)

set_tests_properties (test_5_2
	PROPERTIES PASS_REGULAR_EXPRESSION "is 25")
```

2. 说明
	
	- `test_run` 用来测试程序是否成功运行并返回 0 值
	- `PASS_REGULAR_EXPRESSION` 用来测试输出是否包含后面跟着的字符串

3. 运行：

	`make test`

---

## 生成安装包

1. 配置  

首先在顶层的 CMakeLists.txt 文件尾部添加下面几行：
```
# 构建一个 CPack 安装包
include (InstallRequiredSystemLibraries)
set (CPACK_RESOURCE_FILE_LICENSE
	"${CMAKE_CURRENT_SOURCE_DIR}/License.txt")
set (CPACK_PACKAGE_VERSION_MAJOR "${Demo_VERSION_MAJOR}")
set (CPACK_PACKAGE_VERSION_MINOR "${Demo_VERSION_MINOR}")
include (CPack)
```

导入 InstallRequiredSystemLibraries 模块，以便之后导入 CPack 模块；  
设置一些 CPack 相关变量，包括版权信息和版本信息；  
导入 CPack 模块。
2. 构建工程，并执行 cpack 命令。

- 生成二进制安装包：  
	`cpack -C CPackConfig.cmake`
- 生成源码安装包  
	`cpack -C CPackSourceConfig.cmake`

---

## CMAKE系统变量

| 标识符 | 描述 |
|  ---  | --- |
| PROJECT_NAME | 工程名 ${PROJECT_NAME} |
| VERSION | 版本号 VERSION 1.0.2 |
| INTERFACE | 表示消费者 需要 生产者不需要 |
| PRIVATE | 表示消费者不需要生产者需要 |
| PUBLIC | 表示消费者和生产者都需要 |
| EXECUTABLE_OUTPUT_PATH | 生成的可执行文件的的目录 |

---

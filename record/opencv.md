# opencv
开源的计算机视觉和机器学习库
官网：[OpenCV](https://opencv.org/)

# 编译安装
## 环境
* windows 10 x64
* cuda 11.4
* cudnn 8
* Qt 5.15.2
* Visual Studio 2019 (MSVC16)
* Cmake 3.27

## 下载源码
1. opencv: [release 下载](https://opencv.org/releases/)
2. opencv-contrib: [github 下载](https://github.com/opencv/opencv_contrib/tags)

## cmake配置
1. 启动cmake-gui 选择opencv源文件，选择构建目录，开启advanced
2. config配置选择编译器，这里选择Visual Studio 16 2019，等待构建
3. 搜索cuda,勾选cuda相关选项
4. 搜索qt,勾选qt相关选项
5. 搜索mo,指定modules path的路径，即opencv-contrib/modules的路径
6. 搜索opengl,勾选opengl相关选项
7. 点击configure,等待构建完成
8. 搜索cuda，将CUDA_ARCH_BIN改为自己显卡的算力（可选，轻量化）
9. 将BUILD_opencv_cudacodec 取消勾选，没有安装nvidia video sdk的话
10. 搜索java,取消勾选java构建（可选，轻量化）
11. 搜索python,取消勾选python构建（可选，轻量化）
12. 搜索test,取消勾选test构建（可选，轻量化）
13. 搜索math，勾选两个fast math
14. 点击configure,等待构建完成
15. 处理报错，比如相关包下载失败等
16. 再次点击configure,直到无报错，构建完成
17. 点击Generate,无报错
18. 点击Open Project,进入Visual Studio 2019

## Visual Studio编译
1. 选择编译版本，Debug、Release
2. 展开CmakeTargets，右键ALL_BUILD,点击**生成**，开始编译
3. 等待编译完成，时长2～4个小时
4. 编译成功，无报错，右键INSTALL,点击**生成**，安装导出库文件
5. 等待执行完成，时长5～20分钟
6. 执行成功，无报错，OpenCV C++库编译完成
7. 打开工程目录，库文件在install文件夹内

# 相关问题解决
1. Policy CMPxxxx is not set
CMPxxxx 为具体代码如 CMP0146
添加设置
```
if(POLICY CMPxxxx)
	cmake_policy(SET CMPxxxx OLD)
endif()
```

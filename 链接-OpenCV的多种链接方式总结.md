# 链接问题-OpenCV的多种链接方式总结

```cmake
# find_package方式
cmake_minimum_required(VERSION 2.8)
project(Opencv-AstroWYH)
find_package(OpenCV 3 REQUIRED)

message(STATUS "OpenCV_DIR = ${OpenCV_DIR}") 
# /usr/local/share/OpenCV
message(STATUS "OpenCV_INCLUDE_DIRS = ${OpenCV_INCLUDE_DIRS}") 
# /usr/local/include;/usr/local/include/opencv
message(STATUS "OpenCV_LIBS = ${OpenCV_LIBS}") 
# 库名，如opencv_calib3d;opencv_core;...

include_directories(${OPENCV_INCLUDE_DIRS}) # 头文件包含路径
add_executable(opencv_test ${src})
target_link_libraries(opencv_test ${OpenCV_LIBS}) # 链接库
# -------------------------------------------------------------------------------------
# Android方式
if(ANDROID)
	INCLUDE_DIRECTORIES(${project_root_dir}/third_party/.../opencv/include) # 头文件包含路径
if(ANDROID)
	INCLUDE(${project_root_dir}/third_party/.../opencv/opencv.cmake) # 定义了库名、库路径等
add_executable(opencv_test ${src})
target_link_libraries(opencv_test ${opencv_all}) # 链接库
```


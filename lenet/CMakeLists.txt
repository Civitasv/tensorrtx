cmake_minimum_required(VERSION 3.20)

project(lenet)

set(TARGET_NAME "lenet")

option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_BUILD_TYPE Debug)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

set(TENSORRT_INCLUDE_DIR "D:/TensorRT-8.6.1.6/include")
set(CUDA_INCLUDE_DIR "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.7/include")
set(CUDNN_INCLUDE_DIR "C:/Program Files/NVIDIA/CUDNN/v8.x/include")

set(CUDA_LINK_DIR "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v11.7/lib/x64")
set(TENSORRT_LINK_DIR "D:/TensorRT-8.6.1.6/lib")
set(CUDNN_LINK_DIR "C:/Program Files/NVIDIA/CUDNN/v8.x/lib")

include_directories(${PROJECT_SOURCE_DIR}/include)
# include and link dirs of cuda and tensorrt, you need adapt them if yours are different
# cuda
include_directories(${CUDA_INCLUDE_DIR})
link_directories(${CUDA_LINK_DIR})
# tensorrt
include_directories(${TENSORRT_INCLUDE_DIR})
link_directories(${TENSORRT_LINK_DIR})

FILE(GLOB SRC_FILES ${PROJECT_SOURCE_DIR}/lenet.cpp ${PROJECT_SOURCE_DIR}/include/*.h)

add_executable(${TARGET_NAME} ${SRC_FILES})
target_link_libraries(${TARGET_NAME} nvinfer.lib)
target_link_libraries(${TARGET_NAME} cudart.lib)

add_definitions(-pthread)

cmake_minimum_required(VERSION 3.13)
project(TensorRT_test)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)
 
set(SAMPLES_COMMON_SOURCES "/usr/local/TensorRT-8.6.1.6/samples/common/logger.cpp") 
add_executable(TensorRT_test_OnnxMNIST sampleOnnxMNIST.cpp ${SAMPLES_COMMON_SOURCES})
 
# add TensorRT8
include_directories(/usr/local/TensorRT-8.6.1.6/include)
include_directories(/usr/local/TensorRT-8.6.1.6/samples/common)
set(TENSORRT_LIB_PATH "/usr/local/TensorRT-8.6.1.6/lib")
file(GLOB LIBS "${TENSORRT_LIB_PATH}/*.so")
 
# add CUDA
find_package(CUDA 11.8 REQUIRED)
message("CUDA_LIBRARIES:${CUDA_LIBRARIES}")
message("CUDA_INCLUDE_DIRS:${CUDA_INCLUDE_DIRS}")
include_directories(${CUDA_INCLUDE_DIRS})
 
# link
target_link_libraries(TensorRT_test_OnnxMNIST ${LIBS} ${CUDA_LIBRARIES})
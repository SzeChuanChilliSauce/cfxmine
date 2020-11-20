cmake_minimum_required(VERSION 3.10)

project(cfxmine CXX CUDA)

set(THIRDPARTY_SOURCE_DIR ${PROJECT_SOURCE_DIR}/third-party)

set(BOOST_ROOT /usr/local/inlucde/boost)
include_directories(/usr/local/cuda/include)
link_directories(/usr/local/cuda/lib64)

if(NOT DEFINED ${CMAKE_CUDA_ARCHITECTURES})
  set(CMAKE_CUDA_ARCHITECTURES 61 75)
endif()

find_package(CUDAToolkit)

set(Boost_USE_STATIC_LIBS ON)
# set(Boost_DEBUG ON)
find_package(Boost 1.65.1 REQUIRED COMPONENTS chrono regex system thread)

add_subdirectory(${THIRDPARTY_SOURCE_DIR}/jsoncpp)

add_executable(cfxmine
  src/main.cc
  src/StratumClient.cc
  src/light.cc
  src/sha3.cc
  src/OctopusCPUMiner.cc
  src/OctopusCUDAMiner.cu
)
set_property(TARGET cfxmine PROPERTY CXX_STANDARD 17)
target_include_directories(
  cfxmine
  PUBLIC
  ${THIRDPARTY_SOURCE_DIR}/cxxopts/include
)
target_link_libraries(
  cfxmine
  PUBLIC
  Boost::thread
  Boost::regex
  cudart_static
  jsoncpp_lib
)

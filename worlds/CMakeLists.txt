cmake_minimum_required(VERSION 3.10.2 FATAL_ERROR)

project(avoid_wall)

find_package(ignition-transport11 REQUIRED)

include_directories(${CMAKE_BINARY_DIR})

add_executable(lidar_node lidar_node.cc)

target_link_libraries(lidar_node
  ignition-transport11::core
)
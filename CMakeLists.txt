cmake_minimum_required(VERSION 3.29)
project(HyprViewd)

find_package(fmt REQUIRED)

set(CMAKE_CXX_STANDARD 23)
add_subdirectory(src)
install(TARGETS hypr-viewd DESTINATION bin)

set(CMAKE_BUILD_TYPE Debug)  # Ensures debug info
set(CMAKE_CXX_FLAGS "-g -O0")  # Adds debug symbols and disables optimizations

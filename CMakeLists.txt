cmake_minimum_required(VERSION 3.29)
project(HyprViewd)

# Set C++ version
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Dependencies
find_package(fmt REQUIRED)

# Manually locate wlroots
find_library(WLROOTS_LIBRARY NAMES wlroots)
find_path(WLROOTS_INCLUDE_DIR NAMES wlr/backend.h)

if(NOT WLROOTS_LIBRARY OR NOT WLROOTS_INCLUDE_DIR)
    message(FATAL_ERROR "wlroots not found! Ensure it's installed in your environment.")
endif()

# Add source directory
add_subdirectory(src)

# Define executable
add_executable(hypr-viewd src/main.cpp)

# Link libraries
target_include_directories(hypr-viewd PRIVATE ${WLROOTS_INCLUDE_DIR})
target_link_libraries(hypr-viewd PRIVATE ${WLROOTS_LIBRARY} fmt)

# Installation
install(TARGETS hypr-viewd DESTINATION bin)

# Debugging
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_CXX_FLAGS "-g -O0")  # Adds debug symbols and disables optimizations


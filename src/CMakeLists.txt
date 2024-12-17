cmake_minimum_required(VERSION 3.10)

project(croppy VERSION 0.0.1 LANGUAGES C CXX)

include_directories(${CMAKE_SOURCE_DIR}/kiwi)

# Force libc++ and set C++17 standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -fPIC -Wno-error=pointer-to-int-cast -D__ANDROID_API__=24")

# Ensure NDK and platform compatibility
set(CMAKE_SYSTEM_VERSION 24)

# Define uintptr_t for proper casting
add_definitions(-Duintptr_t=unsigned long)

add_library(croppy SHARED
  "fit_polygon_in_quad.cpp"
  "croppy.c"
)

set_target_properties(croppy PROPERTIES
  PUBLIC_HEADER croppy.h
  OUTPUT_NAME "croppy"
)

target_compile_definitions(croppy PUBLIC DART_SHARED_LIB)
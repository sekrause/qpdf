

cmake_minimum_required(VERSION 3.15)
cmake_policy(SET CMP0091 NEW)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

project(qpdf)

set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

find_package(JPEG REQUIRED)
find_package(ZLIB REQUIRED)

include_directories(include external-libs/include)

add_subdirectory(libqpdf)
add_subdirectory(qpdf)

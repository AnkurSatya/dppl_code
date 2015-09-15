# CMakeLists
cmake_minimum_required(VERSION 3.1)
project (dubinsAreaCoverage CXX)

enable_testing()

find_library(OGDF ogdf)
find_library(COIN coin)

## Set c++11 (c++0x)
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

## Make binaries output in the same directory
#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

## Paths to includes and libraries
link_directories( ${CMAKE_SOURCE_DIR}/lib/LKH )
link_directories( ${CMAKE_SOURCE_DIR}/lib/ogdf/_debug )

include_directories( ${CMAKE_SOURCE_DIR}/lib/ogdf/include )
include_directories( ${CMAKE_SOURCE_DIR}/lib/eigen-eigen-bdd17ee3b1b3 )
#include_directories( ${CMAKE_SOURCE_DIR}/lib/cxxopts/src )
include_directories( ${CMAKE_SOURCE_DIR}/lib/LKH/src/include )
include_directories( ${CMAKE_SOURCE_DIR}/include )

## Add subdirectories
add_subdirectory( src )
add_subdirectory( test )

## Add Compiler Flags

# OSX
add_definitions("-fno-pie")

#SET( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${GCC_COVERAGE_COMPILE_FLAGS} -g" )


# the compiler used for C files 
MESSAGE( STATUS "CMAKE_C_COMPILER: " ${CMAKE_C_COMPILER} )

# the compiler used for C++ files 
MESSAGE( STATUS "CMAKE_CXX_COMPILER: " ${CMAKE_CXX_COMPILER} )

# if the compiler is a variant of gcc, this should be set to 1 
MESSAGE( STATUS "CMAKE_COMPILER_IS_GNUCC: " ${CMAKE_COMPILER_IS_GNUCC} )

# if the compiler is a variant of g++, this should be set to 1 
MESSAGE( STATUS "CMAKE_COMPILER_IS_GNUCXX : " ${CMAKE_COMPILER_IS_GNUCXX} )
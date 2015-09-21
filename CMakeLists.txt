project(GraphLab)

# We require the most recent version of cmake and automatically
# install the correct version when using the cmake lists
cmake_minimum_required(VERSION 2.8.3)

# Libraries linked via full path no longer produce linker search paths.
cmake_policy(SET CMP0003 NEW)
# Preprocessor definition values are now escaped automatically.
cmake_policy(SET CMP0005 NEW)

# for cmake 3.0
if(${CMAKE_MAJOR_VERSION} GREATER 2)
cmake_policy(SET CMP0045 OLD)
cmake_policy(SET CMP0046 OLD)
endif()

# Determine where additional GraphLab specific cmake modules are
# defined
set(CMAKE_MODULE_PATH ${GraphLab_SOURCE_DIR}/cmake)

# TODO: what is this used by
set(BUILD_SHARED_LIBS ON)

# System Introspection
include(CheckLibraryExists)
include(CheckFunctionExists)
include(ExternalProject)
include(CheckCXXSourceCompiles)

# set include path
include_directories(
  ${GraphLab_SOURCE_DIR}/src
  ${GraphLab_SOURCE_DIR}/cxxtest
  ${GraphLab_SOURCE_DIR}/deps/local/include)

if (APPLE)
  if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    set(APPLE_CLANG false)
    message(STATUS "Using GCC Compiler on Mac")
  else()
    set(APPLE_CLANG true)
    message(STATUS "Using Clang Compiler on Mac")
  endif()
endif()
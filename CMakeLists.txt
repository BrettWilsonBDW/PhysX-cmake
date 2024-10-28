cmake_minimum_required(VERSION 3.22)

# Get project name from directory
# get_filename_component(PROJECT_NAME ${CMAKE_CURRENT_LIST_DIR} NAME)

set(PROJECT_NAME "physx")

# Define project with C++ language
project(${PROJECT_NAME} LANGUAGES CXX)

# Configure debug and release build flags
if (CMAKE_BUILD_TYPE STREQUAL "Debug")
  add_definitions(-D_DEBUG )
else ()
  add_definitions(-DNDEBUG)
endif ()

# Disable CUDA PhysX and enable static PhysX library
add_definitions(-DDISABLE_CUDA_PHYSX -DPX_PHYSX_STATIC_LIB)

add_definitions(-DNO_UNIX)

# Include PhysX header directories
include_directories(${CMAKE_CURRENT_LIST_DIR}/px/include)

# Recursively collect PhysX source include directories
file(GLOB_RECURSE MY_INCLUDE_DIRS LIST_DIRECTORIES true
  ${CMAKE_CURRENT_LIST_DIR}/px/src/*)
include_directories(${MY_INCLUDE_DIRS})

# Collect PhysX source files
file(GLOB_RECURSE PX_LIBRARY_SOURCES
  ${CMAKE_CURRENT_LIST_DIR}/px/src/*.cpp
  ${CMAKE_CURRENT_LIST_DIR}/px/src/*.h
)

set(CMAKE_PDB_OUTPUT_DIRECTORY "")
set(CMAKE_COMPILE_PDB_OUTPUT_DIRECTORY "")
set(CMAKE_EXE_LINKER_FLAGS "/NODEFAULTLIB")

# Create static library
add_library(${PROJECT_NAME} STATIC ${PX_LIBRARY_SOURCES})

cmake_minimum_required(VERSION 3.0)

# Specify your project name here
project(Project)

# Add a local directory for custom CMake modules
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

# Specify compiler options for GCC, Clang, and MSVC
if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU" OR
    ${CMAKE_CXX_COMPILER_ID} STREQUAL "Clang")
    # Compiler options for GCC and Clang on Linus or OSX

    # Use C++ 11
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

    # Set warning levels
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic")

    # Set debug and release flags
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} ${CMAKE_CXX_FLAGS_DEBUG} -g")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} ${CMAKE_CXX_FLAGS_RELEASE} -O2")

elseif (${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
    # Compiler options for MSVC on Windows
    if (CMAKE_CXX_FLAGS MATCHES "/W[0-4]")
        string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
    else()
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
    endif()
endif()

# Use find_package to load CMake modules for locating external libraries.
find_package(foo REQUIRED)

# message is great for printing variables when debugging
# message(STATUS "FOO_LIBRARY...... ${FOO_LIBRARY}")

# Include directories with a CMakeLists.txt
add_subdirectory("${CMAKE_SOURCE_DIR}/src")

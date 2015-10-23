cmake_minimum_required(VERSION 3.0)
project(Project)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "GNU" OR ${CMAKE_CXX_COMPILER_ID} STREQUAL "Clang")
	# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic -std=c++11")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -std=c++11")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS} ${CMAKE_CXX_FLAGS_DEBUG} -g")
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} ${CMAKE_CXX_FLAGS_RELEASE} -O2")
elseif (${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
	if (CMAKE_CXX_FLAGS MATCHES "/W[0-4]")
		string(REGEX REPLACE "/W[0-4]" "/W4" CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
	else()
		set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
	endif()
endif()

# Set the list of Boost components you would like to use. python is required if
# you want to build a Boost.Python project, but you should add any other
# components your project may require.
set(BOOST_COMPONENT_LIST
    python
)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_LIBS OFF)
add_definitions("-DBOOST_ALL_DYN_LINK")

# These CMake modules are included with CMake and required to build a
# Boost.Python project, but naturally you'll need to add lines for any libraries
# your project may require.
find_package(Boost COMPONENTS ${BOOST_COMPONENT_LIST} REQUIRED)
find_package(PythonInterp REQUIRED)
find_package(PythonLibs REQUIRED)

add_subdirectory("${CMAKE_SOURCE_DIR}/src")

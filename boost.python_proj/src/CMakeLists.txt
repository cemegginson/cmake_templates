# Setting the TARGET_NAME and SRC_FILES variables is explained in the C/C++
# project template.
set(TARGET_NAME __foo)

set(SRC_FILES
    foo.cpp
)

# This function handles running add_library, as well as performing some other
# tasks specific to building Boost.Python bindings.
python_add_module(${TARGET_NAME} ${SRC_FILES})

# Including and linking is the same as my standard C/C++ project template,
# though I've left the Boost and Python bits since you'll need them anyways.
target_include_directories(${TARGET_NAME} PRIVATE
                          ${Boost_INCLUDE_DIRS}
                          ${PYTHON_INCLUDE_DIRS}
                          "${CMAKE_SOURCE_DIR}/include"
)

target_link_libraries(${TARGET_NAME}
                     ${Boost_LIBRARIES}
                     ${PYTHON_LIBRARIES}
)

# When install is used (make install or the INSTALL solution in VS) copy the
# binary as well as a basic __init__.py to the folder MyModule. Note that
# the location of MyModule is determined by the CMAKE_INSTALL_PREFIX variable.
install (TARGETS ${TARGET_NAME} DESTINATION MyModule)
install (FILES __init__.py DESTINATION MyModule)

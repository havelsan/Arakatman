cmake_minimum_required(VERSION 3.5)
project(my_package)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# Add the executable
add_executable(my_executable main.cpp)

# Message to output upon build
message(STATUS "Building my_package")

message(STATUS "CATKIN_INSTALL_INTO_PREFIX_ROOT=${CATKIN_INSTALL_INTO_PREFIX_ROOT}")

# Installation steps
install(TARGETS my_executable
    RUNTIME DESTINATION bin
)

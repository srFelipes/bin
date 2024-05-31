cmake_minimum_required(VERSION 3.10)

# Set the project name and version
project(algo VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Set the project structure
set(PROJECT_SOURCE_DIR  src)
set(PROJECT_INCLUDE_DIR include)
set(PROJECT_TEST_DIR test)
set(PROJECT_SCRIPTS_DIR scripts)  # New scripts folder 

# Add library source files
set(LIB_SOURCES
    ${PROJECT_SOURCE_DIR}/algo.cpp
)

# Add library header files
set(LIB_HEADERS
    ${PROJECT_INCLUDE_DIR}/algo.hpp
)

# Create the library
add_library(my_lib ${LIB_SOURCES} ${LIB_HEADERS})

# Find and link against GTest
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Add test executable
add_executable(test_main ${PROJECT_TEST_DIR}/main.cpp)


# Link the test executable with your library, GTest, and pthread
target_link_libraries(test_main my_lib ${GTEST_BOTH_LIBRARIES} pthread)


# Link the test executable with your library and GTest
target_link_libraries(test_main my_lib ${GTEST_BOTH_LIBRARIES})

# Enable testing
enable_testing()
# Add the test to the CTest framework
add_test(NAME my_test COMMAND test_main)

# Include directories
include_directories(include)

#add executable file
add_executable(script_exe ${PROJECT_SCRIPTS_DIR}/main.cpp)

# Link the scripts executable with your library
target_link_libraries(script_exe my_lib) 
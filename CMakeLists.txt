# Cmake version
cmake_minimum_required(VERSION 3.0)

# Project Name and Language
project(google_unit_test CXX)

set(CMAKE_CXX_FLAGS "-O2 -Wall -pthread")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
include_directories(
	${PROJECT_SOURCE_DIR}/include
)

link_directories(
	${PROJECT_SOURCE_DIR}
)

# Google Test
set(CMAKE_CXX_STANDARD 11)

include(FetchContent)

# Configure Dependency on GoogleTest
# You need to update GoogleTest Version (609281088cfefc76f9d0ce82e1ff6c30cc3591e5) often to point to the latest version.
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)

# For Windows
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)


enable_testing()

add_executable(hello_test
    src/hello_test.cpp
    src/sample_func.cpp
)
target_link_libraries(hello_test
    gtest_main
)

include(GoogleTest)
gtest_discover_tests(hello_test)


#add_library(simple_udp SHARED src/simple_udp.cpp)
#
#set(TEST_NAME "udp_pub_test")
#add_executable(${TEST_NAME} 
#	test/${TEST_NAME}.cpp
#   	)
#target_link_libraries(${TEST_NAME}
#)

# Add Subdirectory
#add_subdirectory(src)

# Add Include dir
#target_include_directories(
#	${PROJECT_SOURCE_DIR}/include
#)



# Generate new_object_detection from main.cpp
#add_executable(new_object_detection src/main.cpp)
#add_subdirectory(udp_sample)
#add_subdirectory(multi_threading)

cmake_minimum_required(VERSION 3.16)

project(fin-proto-sse-bin-cpp)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(FETCHCONTENT_BASE_DIR "$ENV{HOME}/_deps" CACHE PATH "Base directory for FetchContent downloads")
include(FetchContent)

include_directories(${PROJECT_SOURCE_DIR}/include)

FetchContent_Declare(
    fin_proto_runtime_bin_cpp
    GIT_REPOSITORY https://github.com/xinchentechnote/fin-proto-runtime-bin-cpp.git
    GIT_TAG        main
    GIT_SHALLOW    TRUE
)

FetchContent_MakeAvailable(fin_proto_runtime_bin_cpp)

find_package(ZLIB REQUIRED)
enable_testing()


add_executable(sse_bin_test ./test/sse_binary_test.cpp)
target_include_directories(sse_bin_test PUBLIC ${PROJECT_SOURCE_DIR})
target_link_libraries(sse_bin_test PUBLIC fin_proto_runtime_bin_cpp)
target_link_libraries(sse_bin_test PUBLIC gtest gtest_main ZLIB::ZLIB)

include(GoogleTest)
gtest_discover_tests(sse_bin_test)

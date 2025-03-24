cmake_minimum_required(VERSION 3.10)

# 项目名称
project(MyTestProject)

# 设置C++标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 添加选项以启用覆盖率和测试
option(ENABLE_COVERAGE "Enable coverage reporting" ON)
option(ENABLE_TESTS "Enable testing" ON)

# 如果启用了覆盖率
if(ENABLE_COVERAGE AND CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    message(STATUS "Coverage enabled")
    add_compile_options(-g -O0 -fprofile-arcs -ftest-coverage)
    add_link_options(--coverage)
endif()

# 添加源文件
set(SOURCE_FILES a.cpp)

# 添加头文件路径
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# 添加可执行文件
add_executable(test_my_add test_my_add.cpp ${SOURCE_FILES})

# 启用测试
if(ENABLE_TESTS)
    enable_testing()
    # 添加测试
    add_test(NAME MyTest COMMAND runTests)
endif()


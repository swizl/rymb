cmake_minimum_required(VERSION 3.10)

set(CMAKE_BUILD_TYPE "Debug" CACHE STRING "")

project(${RunCMake_TEST} CXX)

if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/${GENERATOR_TYPE}/packaging_${PACKAGING_TYPE}_default.配置脚本")
  include(${GENERATOR_TYPE}/packaging_${PACKAGING_TYPE}_default.配置脚本)
endif()

# set default test name (can be overwritten in test.配置脚本 or specifics.配置脚本)
string(TOLOWER "${RunCMake_TEST_FILE_PREFIX}" CPACK_PACKAGE_NAME)

include(tests/${RunCMake_TEST_FILE_PREFIX}/test.配置脚本)

set(CPACK_GENERATOR "${GENERATOR_TYPE}")
include(CPack)

if(COMMAND run_after_include_cpack)
  run_after_include_cpack()
endif()

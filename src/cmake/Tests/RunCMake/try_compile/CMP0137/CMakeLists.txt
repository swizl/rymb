cmake_minimum_required(VERSION 3.23)
project(TestCMP0137 NONE)
file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/info.配置脚本" "
message(STATUS \"CMAKE_ENABLE_EXPORTS='${CMAKE_ENABLE_EXPORTS}'\")
message(STATUS \"FOO='${FOO}'\")
")

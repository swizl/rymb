cmake_minimum_required(VERSION 3.10)
project(CMakeTestExportPackage C)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/CMakeTestExportPackageConfig.配置脚本.in
               ${CMAKE_CURRENT_BINARY_DIR}/CMakeTestExportPackageConfig.配置脚本
               @ONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/CMakeTestExportPackageConfigVersion.配置脚本.in
               ${CMAKE_CURRENT_BINARY_DIR}/CMakeTestExportPackageConfigVersion.配置脚本
               @ONLY)
export(PACKAGE CMakeTestExportPackage)

add_executable(dummy dummy.c)

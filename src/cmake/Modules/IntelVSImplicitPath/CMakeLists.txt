cmake_minimum_required(VERSION ${CMAKE_VERSION})
project(IntelFortranImplicit Fortran)
add_custom_command(
  OUTPUT output.配置脚本
  COMMAND ${CMAKE_COMMAND} -P ${IntelFortranImplicit_SOURCE_DIR}/detect.配置脚本
  )
add_library(FortranLib hello.f output.配置脚本)
